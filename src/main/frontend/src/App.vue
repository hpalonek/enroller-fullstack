<template>
  <div id="app">
    <h1>
      <img src="./assets/logo.svg" alt="Enroller" class="logo">
      System do zapisów na zajęcia
    </h1>
    <div v-if="authenticatedUsername">
      <h2>Witaj {{ authenticatedUsername }}!
        <a @click="logout()" class="float-right  button-outline button">Wyloguj</a>
      </h2>
      <meetings-page :username="authenticatedUsername"></meetings-page>
    </div>
    <div v-else>
    
    	<button @click="registering = false">Zaloguj</button>
    	<button @click="registering = true">Zarejestruj</button>
    
    	<register-form @register="register($event)"
      	v-if="registering"></register-form>
      		
    	<login-form @login="login($event)"
      	v-else></login-form>
      
    </div> 
    
  </div>
</template>

<script>
    import "milligram";
    import LoginForm from "./LoginForm";
    import RegisterForm from "./RegisterForm";
    import MeetingsPage from "./meetings/MeetingsPage";

    export default {
        components: {LoginForm, RegisterForm, MeetingsPage},
        data() {
            return {
                authenticatedUsername: "",
                registering: false,
                dodanyUzytkownik: false
            };
        },
        methods: {
            login(user) {
                this.authenticatedUsername = user.login;
            },
            logout() {
                this.authenticatedUsername = '';
            },
            register(user) {
            	 this.$http.post('participants', user)
            	     .then(response => {
            	    	 //udalo sie
            	         //this.dodanyUzytkownik = true;
            	     })
            	     .catch(response => {
            	         // nie uda�o sie
            	         
            	     });
            	}
        }
    };
</script>

<style>
  #app {
    max-width: 1000px;
    margin: 0 auto;
  }

  .logo {
    vertical-align: middle;
  }
</style>

