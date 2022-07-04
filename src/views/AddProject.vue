<template>
  <form @submit.prevent="handleSubmit">
    <label> Title:</label>
    <input type="text" v-model="title" required>
    <label>Details:</label>
    <textarea v-model="details" required ></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
    data(){
        return{
            title: '',
            details: ''
        }
    },
    methods:{
        handleSubmit(){
            // creates an object and saves it in project 
            let project = {
                title: this.title,
                details: this.details,
                complete: false
            }
            // project is sent as a JSON object to the endpoint
            fetch('http://localhost:3000/projects', {
                method: 'POST',
                // contect type if of type JSON
                headers: {'Content-Type': 'application/json'},
                // this is we send JSOn data 
                body: JSON.stringify(project)
                })
                .then(()=>{
                    // redirects to the home directory
                    this.$router.push('/')
                })// catch any error if there is one
                .catch((err) => console.log(err.message))
        }
    }
}
</script>

<style>
    form{
        background: white;
        padding: 20px;
        border-radius: 10px;
        margin-top: 40%;
      
    }

    label{
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: bold;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }

    input{
        padding: 10px;
        border: 0;
        border-bottom: 1px solid #ddd;
        width: 100%;
        box-sizing: border-box;
        font-size: 16px;
    }

    textarea{
        border: 1px solid #ddd;
        padding: 10px;
        width: 100%;
        box-sizing: border-box;
        height: 100px;
        font-size: 16px;
    }

    form button{
        display: block;
        margin: 20px auto 0;
        background: #00ce89;
        color: white;
        border: 0;
        border-radius: 6px;
        padding: 10px;
        font-size: 16px;
    }
</style>