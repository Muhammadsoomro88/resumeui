<template>
    <div class="container">
    <img src="../assets/person1.jpg" alt="">
    <form @submit="onSubmit" class="add-form form-group">
        <div class="inp">
            <input type="text" v-model="name" name="name" placeholder="Enter Name*">
        </div>
        <div class="inp">
            <input type="text" v-model="position" name="position" placeholder="Enter Position*">
        </div>
        <div class="inp">
            <input type="text" v-model="github" name="github" placeholder="Enter Github link*">
        </div>
        <div class="inp">
            <input type="text" v-model="email" name="email" placeholder="Enter Email*">
        </div>
        <div class="inp">
            <input type="text" v-model="linkedin" name="linkedin" placeholder="Enter LinkedIn profile*">
        </div>
        <div class="inp">
            <input type="text" v-model="phone" name="phone" placeholder="Enter Phone*">
        </div>
        <div class="inp">
            <input type="text" v-model="location" name="location" placeholder="Enter Location*">
        </div>
        <div class="inp">
            <textarea name="summary" v-model="summary" id="summary" cols="54" rows="05" placeholder="Enter Personal Objective*"></textarea>
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
    name: 'personal info',
    data(){
        return{
            name: '',
            position: '',
            github: '',
            email: '',
            linkedin: '',
            phone: '',
            location: '',
            summary: '',
            isError: false,
            errorMsg: '',
            buttonValue: 'Add +',
            submitted: false
        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault()
            if (this.name === '' || this.position === '' || this.github === '' || this.email === '' || 
                this.linkedin === '' || this.phone === '' || this.location === '' || this.summary === '') {
                this.isError = true
                this.errorMsg = '*missing required field'
                return
            }
            else{
                this.isError = false
            }
            const createdEmp = {
                name: this.name,
                position: this.position,
                github: this.github,
                email: this.email,
                linkedin: this.linkedin,
                phone: this.phone,
                location: this.location,
                summary: this.summary,
            }
            this.buttonValue = 'Added ✓'
            this.submitted = true
            this.$emit('created-task', createdEmp)
        }
    }
}
</script>

<style scoped>
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
input[type='text']:hover{
    border: none;
    border-bottom: 2px solid black;
}
.container{
    border: 2px solid black;
    max-width: 600px;
}
img{
    max-height: 100px;
    max-width: 100px;
}
textarea{
    border: 1px solid black;
}
p{
    color: crimson;
    font-weight: bold;
}
</style>