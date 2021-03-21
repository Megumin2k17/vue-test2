<template>  
  <div class="container column">
    <app-resume-create @resumeId="getResume"></app-resume-create>
    

    <app-resume-view :resume="resume"></app-resume-view>
  </div>
  
  <app-resume-comments></app-resume-comments>
  
</template>

<script>

import AppResumeCreate from './components/AppResumeCreate'
import AppResumeView from './components/AppResumeView'
import AppResumeComments from './components/AppResumeComments'

export default {
  data() {
    return {
      resume:null,
      commetns: []
    }
  }, 
  methods: {
    
    async getResume(resumeId) {

      const resume = await fetch(`https://test2-b03bb-default-rtdb.firebaseio.com/resume/${resumeId}.json`).then((response) => { return response.json() })
      
      this.resume = resume 
      
    }

  },
  components: {
    AppResumeCreate, AppResumeView, AppResumeComments
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
