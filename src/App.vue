<template>
 <div id="app">
  <b-nav-item class="nav-link active" :to="{ name: 'main' }"><img src="@/Images/LogoSite.jpg" style="height:100px"></b-nav-item>
  <nav class="navbar navbar-expand-lg navbar-light" style="background-color:#F5F5F5; margin-top: -100px; margin-left: 150px;" >
    <ul class="navbar-nav" >
      <li class="nav-item active">
        <b-nav-item class="nav-link active" :to="{ name: 'main' }">Home</b-nav-item>
      </li>
      <li class="nav-item active">
         <b-nav-item class="nav-link active" :to="{ name: 'search' }">Search</b-nav-item>
      </li>
      <li class="nav-item active">
         <b-nav-item class="nav-link active" :to="{ name: 'about' }">About</b-nav-item>
      </li>
    </ul>
  </nav>
  <nav class="navbar navbar-expand-lg navbar-light" style="margin-top: -72px; margin-left: 1500px;background-color:#F5F5F5" v-if="!$root.store.username"  >
    <ul class="navbar-nav"  >
        <li class="nav-item active"  >
         <b-nav-item class="nav-link active"  ><b-icon-person-circle></b-icon-person-circle> <span >Hello Guest!</span></b-nav-item>
         </li>
         <li>
         <b-nav-item class="nav-link active" :to="{ name: 'register' }">Register</b-nav-item>
         </li>
          <li>
         <b-nav-item class="nav-link active" :to="{ name: 'login' }">Login</b-nav-item>
         </li>
    </ul>
  </nav>
  <nav class="navbar navbar-expand-lg navbar-light" style="margin-top: -72px; margin-left: 1500px;background-color:#F5F5F5" v-else  >
    <ul class="navbar-nav"  >
      <li class="nav-item active"  >
        <b-nav-item class="nav-link active"  ><b-icon-person-circle></b-icon-person-circle> <span >Hello,{{$root.store.username}} !</span></b-nav-item>
      </li>
      <li> 
        <b-dropdown id="dropdown-1" text="Personal" class="m-md-2"  >
          <b-dropdown-item :to="{ name: 'register' }">Favorites</b-dropdown-item>
          <b-dropdown-item :to="{ name: 'register' }">Private</b-dropdown-item>
          <b-dropdown-item :to="{ name: 'register' }">Family Recipe</b-dropdown-item>
          <b-dropdown-item v-b-modal="'modal-prevent-closing'">Create Recipe</b-dropdown-item>
        </b-dropdown>
      <CreateRecipe></CreateRecipe>  
      </li>
      <li>
        <b-nav-item class="nav-link active"  @click="Logout">Logout</b-nav-item>
      </li>
    </ul>
  </nav>
  <div id="nav">
  </div>
  <router-view />
  </div>
</template>

<script>
//How to run the app?
//1.Open terminal
//2.npm install
//3.npm run serve
import CreateRecipe from "./components/CreateRecipe.vue";
export default {
  name: "App",
  components:{
    CreateRecipe
  },
  methods: {
    Logout() {
       
      this.$root.store.logout();

      this.$root.toast("Logout", "User logged out successfully", "success");
      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}
#nav-link{
  color:black;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
.nav-link active{
color: black;
}
</style>
