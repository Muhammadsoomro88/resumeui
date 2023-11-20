<template>
  <div class="container">
    <img src="../assets/work.png" alt="">
    <form @submit="onSubmit" class="add-form">
        <a @click="incrementIteration">+add job</a>
        <br>
        <div v-for="num in iterate" :key="num">
            <div class="inp">
                <input type="text" v-model="position" name="position" placeholder="Enter Position*">
            </div>
            <div class="inp">
                <input type="text" v-model="company" name="company" placeholder="*Enter Company Name*">
            </div>
            <div class="inp">
                <input style="border:1px solid black;max-width:140px;" type="text" v-model="start" name="start" placeholder="Start Date*">&nbsp;&nbsp;&nbsp;&nbsp;
                <input type="text" style="border:1px solid black;max-width:140px" v-model="end" name="end" placeholder="End Date*" :readonly="present">
                <div class="form-control-check">
                    <label><input type="checkbox" v-model="present" name="present">Present</label>
                </div>
            </div>
            <div class="inp">
                <textarea name="summary" v-model="summary" id="summary" cols="54" rows="05" placeholder="Enter Job Summary*"></textarea>
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
    name: 'jobInfo',
    data(){
        return{
            iterate: 1,
            position: '',
            company: '',
            start: '',
            end: '',
            summary: ``,
            present: false,
            jobDetails: [],
            isError: false,
            errorMsg: '',
            buttonValue: 'Add +',
            submitted: false
        }
    },
    methods:{
        incrementIteration(){
            this.iterate = this.iterate+1
            if (this.present) {
                this.end = 'Present'
            }
            const createdEmp = {
                position: this.position,
                company: this.company,
                start: this.start,
                end: this.end,
                summary: this.summary
            }
            this.jobDetails.push(createdEmp)
        },
        onSubmit(e){
            e.preventDefault()
            if (this.present) {
                this.end = 'Present'
            }

            if (this.position === '' || this.company === '' || this.start === '' || this.end === '' || this.summary === '' ){
                this.isError = true
                this.errorMsg = '*missing required field'
                return
            }
            else{
                this.isError = false
            }
            
            const createdEmp = {
                position: this.position,
                company: this.company,
                start: this.start,
                end: this.end,
                summary: this.summary
            }
            this.jobDetails.push(createdEmp)
            this.buttonValue = 'Added ✓'
            this.submitted = true
            this.$emit('job-details', this.jobDetails)
        },
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