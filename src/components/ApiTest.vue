<template>
    <section class="box">
        <button @click="sendGetRequest">Send Get Request</button>
        <br>
        <button @click="sendPostRequest">Send Post Request</button>

        <p>{{someData}}</p>
    </section>
</template>

<script>
import axios from 'axios';

export default {
data(){
    return{
        someData: 'This works!',
        emailData: "eve.holt@reqres.in",
        passwordData: "pistol"
    }
},
methods: { 
    sendGetRequest(){
        axios.get("https://reqres.in/api/users")
        .then(response =>{
            console.log(response);
        })
    },

    sendPostRequest(){
        axios.post("https://reqres.in/api/register",
        {
            "email": this.emailData,
            "password": this.passwordData
        })
        .then(response => {
            console.log(response);
        });
    }
}
}
</script>

<style scoped>
.box{
height: 100vh;
width: 100%;
background-color: lightgray;
}
button, p{
    margin-top: 30px;
    margin-left: 30px;
}
</style>

