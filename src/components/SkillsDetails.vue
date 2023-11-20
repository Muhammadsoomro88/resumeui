<template>
<div class="container">
    <img src="../assets/skill.png" alt="">
    <form @submit="onSubmit" class="add-form">
        <div class="inp">
            <input type="text" v-model="skills" name="skills" placeholder="Enter Skills*">
            <p>*add skills separated by a ','</p>
        </div>
        <a @click="incrementIteration">+add achievement</a>
        <br>
        <div v-for="num in iterate" :key="num">
            <div class="inp">
                <input type="text" v-model="title" name="title" placeholder="Enter Achievement*">
            </div>
            <div class="inp">
                <textarea name="details" v-model="details" id="details" cols="54" rows="05" placeholder="Enter Details*"></textarea>
            </div>
            <div v-if="isError">
                <bold><h5>{{errorMsg}}</h5></bold>
            </div>
            </div>
        <div>
            <input type="submit" :class="[submitted?'btn-success':'btn-primary', 'btn']" name="create" :value="buttonValue">
        </div>
    </form>
</div>
</template>

<script>
export default {
    name: 'skillDetails',
    data(){
        return{
            iterate: 1,
            skills: '',
            title: '',
            details: '',
            achievements: [],
            skillsInfo: [],
            isError: false,
            errorMsg: '',
            buttonValue: 'Add +',
            submitted: false
        }
    },
    methods:{
        incrementIteration(){
            this.iterate = this.iterate + 1
            const achievementDetails = {
                title: this.title,
                details: this.details
            }
            this.achievements.push(achievementDetails)
        },
        onSubmit(e){
            e.preventDefault()
            if(this.skills === '' || this.title === '' || this.details === ''){
                this.isError = true
                this.errorMsg = '*missing required field'
                return
            }
            else{
                this.isError = false
            }

            const achievementDetails = {
                title: this.title,
                details: this.details
            }
            this.achievements.push(achievementDetails)
            const combined = {
                skills: this.skills,
                achievements: this.achievements
            }
            this.buttonValue = 'Added ✓'
            this.submitted = true
            this.$emit('skill-details',  combined)
        }
    }
}
</script>

<style scoped>
img{
    max-height: 100px;
    max-width: 100px;
}
.form-control-check{
    margin-left: 90px;
}
p{
    float: left;
    margin-left:57px;
    font-size: 13px;
    opacity: 0.7;
}
h5{
    color: crimson;
    font-weight: bold;
    font-size: 15px;
}
a{
    color: white;
}
</style>