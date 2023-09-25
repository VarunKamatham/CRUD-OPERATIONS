<template>
<div class="Banner">
 <img class="logo" src="../assets/logo1.jpg">
 <h1>Sign Up</h1>
 <div class="register">
    <input type="text" v-model="name" placeholder="Enter name"/>
    <input type="text" v-model="email" placeholder="Enter email"/>
    <input type="password" v-model="password" placeholder="Enter password"/>
    <button v-on:click="signUp">SignUp</button>
    <p><router-link to="/login">Login</router-link></p>
 </div>
</div>
</template>
<script>
import axios from 'axios';
export default {
    name : 'SignUp',
    data(){
        return{
            name :"",
            email :"",
            password : ""
        }
    },
    mounted(){
        let user= localStorage.getItem('user-info');
        if(user){
            this.$router.push({name :'Home'})
        }
    },
    methods:{
        async signUp() {
            let result = await axios.post("http://localhost:3000/users" ,{
                email:this.email,
                password:this.password,
                name:this.name
            });
            console.warn(result);
            if(result.status==201){
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:'Home'})
            }
        }
    }
}
</script>
<style scoped>
.Banner{
    background-image: url("../assets/Banner.jpg");
    width: 100%;
    height: 788px;
    background-repeat: no-repeat;
    background-size: cover;
}
</style>
