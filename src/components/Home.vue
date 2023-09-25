<template>
<Header/>
    <h1>Hello {{name}}, Welcome to Home Page</h1>
    <table border="1">
        <tr>
            <td>ID</td>
            <td>Name</td>
            <td>Contact</td>
            <td>Address</td>
            <td>Action</td>
        </tr>
        <tr v-for="item in restaurant" :key="item.id">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.contact}}</td>
            <td>{{item.address}}</td>
            <td><router-link :to="'/update/'+item.id">Update</router-link>&nbsp;
            <button v-on:click="deleteRestaurant(item.id)">Delete</button>
            </td>

        </tr>
    </table>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
    name:"Home",
    data(){
        return {
            name :'',
            restaurant:[],
        }
    },
    components:{
        Header
    },
    methods:{
        async deleteRestaurant(id){
        let result = await axios.delete("http://localhost:3000/restsurant/"+id);
        console.warn(result)
        if(result==200){
        this.loadData();
        }
        }
    },
    async loadData(){
        let user= localStorage.getItem('user-info');
        this.name = JSON.parse(user).name;
        if(!user){
            this.$router.push({name :'SignUp'})
        }
        let result = await axios.get("http://localhost:3000/restsurant");
        console.warn(result);
        this.restaurant = result.data;
        location.reload();
    },
    async mounted(){
        // this.loadData();
        let user= localStorage.getItem('user-info');
        this.name = JSON.parse(user).name;
        if(!user){
            this.$router.push({name :'SignUp'})
        }
        let result = await axios.get("http://localhost:3000/restsurant");
        console.warn(result);
        this.restaurant = result.data;
    }
}
</script>
<style>
td{
    width: 160px;
    height: 40px;
}
</style>