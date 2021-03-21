<template>
	
	<div class="card card-w70" v-if="resume">
	 
      <div v-for="item in resume" :key="item">
      	<component :is="'app-resume-'+ item.type" :[item.type]="item.value"></component>
      </div>
      
    </div>

    <div class="card card-w70" v-else><h3>Добавьте первый блок, чтобы увидеть результат</h3></div>
  
</template>


<script>
import AppResumeTitle from './particles/AppResumeTitle'
import AppResumeAvatar from './particles/AppResumeAvatar'
import AppResumeSubtitle from './particles/AppResumeSubtitle'
import AppResumeText from './particles/AppResumeText'

export default {
	props:['resume'],
 	components: { AppResumeTitle, AppResumeAvatar, AppResumeSubtitle, AppResumeText }
}
</script>