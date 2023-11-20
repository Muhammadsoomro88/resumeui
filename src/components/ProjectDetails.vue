<template>
  <div class="container">
    <img src="../assets/laptop.jpg" alt="">
    <form @submit="onSubmit" class="add-form">
        <a @click="incrementIteration">+add project</a>
        <br>
        <div v-for="num in iterate" :key="num">
            <div class="inp">
                <input type="text" v-model="title" name="title" placeholder="Enter Project Name*">
            </div>
            <div class="inp">
                <textarea name="details" v-model="details" id="details" cols="54" rows="05" placeholder="Enter Project Details*"></textarea>
            </div>
            </div>
            <div v-if="isError">
                <bold><p>{{errorMsg}}</p></bold>
            </div>
        <div>
            <input type="submit" :class="[submitted?'btn-success':'btn-primary', 'btn']" name="create" :value="buttonValue">
        </div>
    </form>
</div>
</template>

<script>
export default {
    name: 'projectDetails',
    data(){
        return{
            iterate: 1,
            title: '',
            details: ``,
            projDetails: [],
            isError: false,
            errorMsg: '',
            buttonValue: 'Add +',
            submitted: false
        }
    },
    methods:{
        incrementIteration(){
            this.iterate = this.iterate + 1
            const project = {
                title: this.title,
                details: this.details
            }
            this.projDetails.push(project)
        },
        onSubmit(e){
            e.preventDefault()
            if(this.title === '' || this.details === ''){
                this.isError = true
                this.errorMsg = '*missing required field'
                return
            }
            else{
                this.isError = false
            }
            const project = {
                title: this.title,
                details: this.details
            }
            this.projDetails.push(project)
            this.buttonValue = 'Added ✓'
            this.submitted = true
            this.$emit('project-details', this.projDetails)
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
    color: crimson;
    font-weight: bold;
}
a{
    color: white;
}
</style>