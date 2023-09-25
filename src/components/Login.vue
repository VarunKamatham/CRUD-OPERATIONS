<template>
<div class="Banner">
    <img class="logo" src="../assets/logo1.jpg">
    <h1>Login</h1>
    <div class="login">
    <input type="text" v-model="email" placeholder="Enter email"/>
    <input type="password" v-model="password" placeholder="Enter password"/>
    <button v-on:click="login">Login</button>
    <p><router-link to="/sign-up" style="color:white">Sign Up</router-link></p>
    </div>
</div>
</template>
<script>
import axios from 'axios';
export default {
    name :'Login',
    data(){
        return{
            email:'',
            password:''
        }
    },
     mounted(){
        let user= localStorage.getItem('user-info');
        if(user){
            this.$router.push({name :'Home'})
        }
    },
    methods:{
       async login(){
        let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
        console.warn(result);
        if(result.status==200 && result.data.length>0){
                localStorage.setItem("user-info",JSON.stringify(result.data[0]))
                this.$router.push({name:'Home'})
            }
       }
    }
}
</script>
<style scoped>
.Banner{
    background-image: url("../assets/Bann.png");
    width: 100%;
    height: 788px;
    background-repeat: no-repeat;
    background-size: cover;
}
</style>