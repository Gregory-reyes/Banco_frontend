<template>
  <div id="app" class="app">
    <div class="header">
        <h1><img width="90" height="90" src="https://img.icons8.com/dusk/64/pets.png" alt="pets"/> Banco Happy Pets </h1>
        <nav>
            <button v-if="is_auth" v-on:click="loadHome" > Inicio </button>
            <button v-if="is_auth" v-on:click="loadAccount"> Cuenta </button>
            <button v-if="is_auth" v-on:click="logOut"> Cerrar Sesión </button>
            <button v-if="!is_auth" v-on:click="loadLogIn"> Iniciar Sesión  </button>
            <button v-if="!is_auth" v-on:click="loadSignUp"> Registrarse </button> 
        </nav>
    </div>
  </div>
  <div class="main-component">
    <router-view 
      v-on:completedLogIn= "completedLogIn"
      v-on:completedSignUp= "completedSignUp"
      v-on:logOut="logOut"
      ></router-view>
  </div>
  <div class="footer">
      <h2> Derechos reservados Desarrollo e innovación © </h2>
  </div>    
</template>

<script>
export default({

  data: function(){
      return{
        is_auth: false
      }
  },

  methods:{
    veryAuth: function(){
      this.is_auth= localStorage.getItem("isAuth") || false;

      if(this.is_auth== false)
        this.$router.push({name:"logIn"});
      else
        this.$router.push({name:"home"});
    },  
    loadLogIn: function(){
        this.$router.push({name:"logIn"})
    },
    loadSignUp: function(){
        this.$router.push({name:"signUp"})
    },

    completedLogIn: function(data){
        
        localStorage.setItem("isAuth", true);
        localStorage.setItem("username", data.username);
        localStorage.setItem("token_access", data.token_acess);
        localStorage.setItem("token_refresh", data.token_refresh);
        alert("Auntentificación Exitosa");
        this.veryAuth();
    },

    completedSignUp: function(data){
        alert("Registro Exitoso");
        this.completedLogIn(data);
    },
    logOut:function(){
      localStorage.clear();
      alert("Sesión cerrada");
      this.veryAuth();
    },
    loadHome:function(){
      this.$router.push({name:"home"});
    },
    loadAccount: function () {
    this.$router.push({ name: "account" });
    },

  },

  created:function(){
    this.veryAuth();
  }
})
</script>


<style>

body{
  margin: 0 0 0 0; 
}

.header{
  margin: 0;
  padding: 0;
  width:100%;
  height: 10vh;
  min-height: 100px;
  background-color: #77a8d9;
  color: #E5E7E9;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header h1{
  width: 30%;
  text-align: center;
}

.header nav button
{
  color: #E5E7E9;
  background: #77a8d9;
  border: 1px solid #E5E7E9;
  border-radius: 5px;
  padding: 10px 20px;
}

.header nav button:hover
{
  color: #77a8d9;
  background: #E5E7E9;
  border: 1px solid #E5E7E9;
}

.main-component
{
  height: 75vh;
  margin: 0%;
  padding: 0%;
  background: #FDFEFE;
}

.footer
{
  margin:0;
  padding:0;
  width: 100%;
  font-size: 14px;
  height: 9vh;
  min-height: 60px;
  background-color: #77a8d9;
  color: #E5E7E9;
}

.footer h2{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>