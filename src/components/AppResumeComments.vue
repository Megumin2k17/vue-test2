<template>
	<div class="container">
	    <p>
	      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
	    </p>
	    <div class="card" v-if="comments">
	      <h2>Комментарии</h2>
	      <ul class="list" v-for="comment in comments" :key="comment">	      	
	        <li class="list-item">
	          <div>
	            <p><strong>{{comment.email}}</strong></p>
	            <small>{{comment.body}}</small>
	          </div>
	        </li>
	      </ul>
	    </div>
	    <div class="loader" v-if="loading"></div>
    </div>
</template>

<script>
	export default {
		data() {
			return {
				comments: null,
				loading: false
			}
		},
		methods: {
			async loadComments() {

				this.loading = true

				const comments = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=15').then((response) => { return response.json() })

				this.comments = comments

				this.loading = false
				
			}
		}
	}
</script>