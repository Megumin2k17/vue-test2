<template>
	
	<form class="card card-w30" @submit.prevent='submitData(draft)'>
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model='blockType'>
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model='text'></textarea>        
      </div>
      

      <button class="btn primary" :disabled="btnDisabler">Добавить</button>
    </form>
</template>


<script>

export default {
	
	emits: [
		'resumeId'
	],
	data() {
		return {
			blockType: 'title',
			text: '',
		    resumeId: null,
		    draft: []
		    
		}
	},
	computed: {
		btnDisabler() {
			return this.text.length < 3
		}
	},
	methods: {
		async submitData(data) {

			this.draft.push({type: this.blockType, value: this.text })	
			
			if(!this.resumeId) {

				await this.postData(data)
					
			} else {
				await this.updateData(data)
			}

			this.$emit('resumeId', this.resumeId)

			this.text = ''
			this.blockType='title'
			 
		},
		async postData(data) {
			//https://test2-b03bb-default-rtdb.firebaseio.com/

			const response = await fetch('https://test2-b03bb-default-rtdb.firebaseio.com/resume.json', {
				method: 'POST',
        		headers: {'Content-Type': 'application/json'},
        		body: JSON.stringify(data)}
        	)

        	const firebaseData = await response.json()

         	this.resumeId = firebaseData.name
      		// console.log(firebaseData.name)
			
		},		
		async updateData(data) {

			const response = await fetch(`https://test2-b03bb-default-rtdb.firebaseio.com/resume/${this.resumeId}.json`, {
				method: 'PUT',
        		headers: {'Content-Type': 'application/json'},
        		body: JSON.stringify(data)}
        	)

        	const firebaseData = await response.json()

      		console.log(firebaseData)
		}

	}
 
}
</script>