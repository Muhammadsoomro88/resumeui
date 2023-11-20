<template>
<div>
  <h1><img class="logo" src="./assets/go.png" alt="">Resume</h1>
  <PersonalDetails @created-task="personalInfo"/>
  <JobDetails @job-details="jobInfo" />
  <StudyDetails @study-details="studyInfo" />
  <ProjectDetails @project-details="projectInfo" />
  <SkillsDetails @skill-details="skillInfo" />
  <div v-if="generate">
    <br>
    <p>your information has been added, click here to generate your Resume</p>
    <button @click="createResume" class="btn btn-success">Generate!</button>
  </div>
</div>
</template>

<script>
import axios from "axios";
import PersonalDetails from './components/PersonalDetails.vue'
import JobDetails from './components/JobDetails.vue'
import StudyDetails from './components/StudyDetails.vue'
import ProjectDetails from './components/ProjectDetails.vue'
import SkillsDetails from './components/SkillsDetails.vue'
export default {
  name: 'App',
  components: {PersonalDetails,JobDetails,StudyDetails,ProjectDetails,SkillsDetails},
  data(){
    return{
      Name: '',
      Position: '',
      Github: '',
      Email: '',
      LinkedIn: '',
      Phone: '',
      Location: '',
      Summary: '',
      Job: [],
      Study: [],
      PersonalProj: [],
      Skills: '',
      Achievements: [],
      generate: false
    }
  },
  methods:{
    personalInfo(data){
        console.log(data)
        this.Name = data.name,
        this.Position = data.position,
        this.Github = data.github,
        this.Email = data.email,
        this.LinkedIn = data.linkedin,
        this.Phone = data.phone,
        this.Location = data.location,
        this.Summary = data.summary
    },
    jobInfo(data){
        console.log(data)
        this.Job = data
    },
    studyInfo(data){
        console.log(data)
        this.Study = data
    },
    projectInfo(data){
        console.log(data)
        this.PersonalProj = data
    },
    skillInfo(data){
        console.log(data)
        this.Skills = data.skills,
        this.Achievements = data.achievements
        this.generate = true
    },
    async createResume(){
      const resume = await axios.post('http://localhost:8081/resume',{
        name: this.Name,
        position: this.Position,
        github: this.Github,
        email: this.Email,
        linkedIn: this.LinkedIn,
        phone: this.Phone,
        location: this.Location,
        summary: this.Summary,
        job: this.Job,
        study: this.Study,
        personalProj: this.PersonalProj,
        skills: this.Skills,
        achievements: this.Achievements
      })
      console.log(resume)
      alert('Resume is downloaded')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.add-form{
    margin-bottom: 40px;
    text-align: center;
}
.inp{
    margin: 30px 0;
}
label{
    display: block;
}
input[type='text']{
    height: 40px;
    width: 450px;
    padding: 3px 7px;
    font-size: 17px;
    border: none;
    border-bottom: 1px solid black;
}
a{
    float: right;
    background-color: green;
    padding: 3px;
    text-decoration: none;
    border-radius: 5px;
}
a:hover{
    color: white;
    cursor: pointer;
}
.container{
    border: 2px solid black;
    max-width: 600px;
}
.logo{
  height: 40px;
  width: 130px;
}
h1{
  font-weight: bold;
}
</style>
