<template>
    <div class="logIn_user">
        <div class="container_logIn_user">
        <h2>Iniciar Sesión</h2>

        <form v-on:submit.prevent="processLogInUser">
            <label id="user_username"> Username:
                   <input type="text" v-model="user.username" placeholder="Username" required> 
            </label>
            <br>
            <label id="user_password"> Password:
                   <input type="password" v-model="user.password" placeholder="Password" required> 
            </label>
            <br>
            <button type="submit"> Iniciar Sesion </button>  
        </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data:function(){
        return{
            user:{
                username:"",
                password:""
            }
        }
    },

    methods:{
        processLogInUser: function(){
            axios.post("https://banco-backend-01-148c70f4307b.herokuapp.com/login/",
            this.user, {header:{}})
            .then((result)=>{
                 let dataLogIn={
                    username: this.user.username,
                    token_access: result.data.access,
                    token_refresh: result.data.refresh,
                 } 
                 this.$emit('completedLogIn', dataLogIn)  
            }).catch((error)=>{
                if(error.response.status=="401")
                    alert("ERROR 401: Credenciales Incorrectas");
            }
            );

        }
    }
}
</script>

<style>
.logIn_user{
    margin: 0;
    padding: 0%;
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.container_logIn_user {
    border: 3px solid #77a8d9;
    border-radius: 10px;
    width: 25%;
    height: 60%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.logIn_user h2{
    color: #77a8d9;
}

.logIn_user form{
    width: 70%;
}
.logIn_user input{
    height: 40px;
    width: 100%;
    box-sizing: border-box;
    padding: 10px 20px;
    margin: 5px 0;
    border: 1px solid #77a8d9;
}
.logIn_user button{
    width: 100%;
    height: 40px;
    color: #E5E7E9;
    background: #77a8d9;
    border: 1px solid #E5E7E9;
    border-radius: 5px;
    padding: 10px 25px;
    margin: 5px 0;
}
.logIn_user button:hover{
    color: #E5E7E9;
    background: crimson;
    border: 1px solid #77a8d9;
}
</style>