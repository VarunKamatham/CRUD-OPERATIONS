
<template>
<Header/>
    <h1>Hello {{name}}, Welcome on Update Restaurant Page</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name"/>
        <input type="text" name="address" placeholder="Enter address" v-model="restaurant.address"/>
        <input type="text" name="contact" placeholder="Enter contact" v-model="restaurant.contact"/>
        <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    </form>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
    name:"Update",
    components:{
        Header
    },
    data(){
        return{
            name:'',
        restaurant:{
            name:'',
            address:'',
            contact:''
        }
        }
    },
    methods:{
         async updateRestaurant(){
           const result = await axios.put("http://localhost:3000/restsurant/"+this.$route.params.id,{
            name:this.restaurant.name,
            address:this.restaurant.address,
            contact:this.restaurant.contact
           });
            if(result.status==200){
                this.$router.push({name:'Home'})
            }
        }
    },
    async mounted(){
        let user= localStorage.getItem('user-info');
        this.name = JSON.parse(user).name;
        if(!user){
            this.$router.push({name :'SignUp'})
        }
        const result = await axios.get("http://localhost:3000/restsurant/"+this.$route.params.id);
        console.warn(result);
        this.restaurant = result.data; 
    }
}
</script>