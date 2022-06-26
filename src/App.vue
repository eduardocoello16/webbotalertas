<template>

<div v-if="!isLoadding" id="loadderbox">
<h2>Hola {{data}}</h2>
<span class="loader"></span>
  <h2>Estamos comprobando que seas miembro del grupo de Alertas Tenerife</h2>
</div>

  <nav  v-if="isLoadding">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view v-if="isLoadding"/>
</template>
<script>

export default {

data() {
    return {
     isLoadding: false,
     data: String
    };
  },
 async  mounted() {
    //Obtener datos bot de la API
    this.data = window.Telegram.WebApp.initDataUnsafe.user.first_name;
   console.log(window.Telegram.WebApp.initDataUnsafe.user);


    
// Set timeout await 2 segundos y cambiar el estado de la variable isLoadding a false
    await new Promise(resolve => setTimeout(resolve, 4000));
    this.isLoadding = true;

  }
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
h2{
  width: 100%;
}
body{

    background-color: var(--tg-theme-bg-color);
}
nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: var(--tg-theme-link-color);
    }
  }
}
html, body{
  height: 100%;
}
#loadderbox{
  display: flex;
  justify-content: center;
 height: 100%;
 flex-wrap: wrap;
  align-items: center;
}
.loader {
        width: 84px;
        height: 84px;
        position: relative;
        overflow: hidden;
      }
      .loader:before , .loader:after {
        content: "";
        position: absolute;
        left: 50%;
        bottom: 0;
        width:64px;
        height: 64px;
        border-radius: 50%;
        background:var(--tg-theme-text-color);
        transform: translate(-50% , 100%)  scale(0);
        animation: push 1.6s infinite ease-out;
      }
      .loader:after {
      animation-delay: 0.8s;
      }
      @keyframes push {
          0% {
            transform: translate(-50% , 100%)  scale(1);
          }
          15% , 25%{
            transform: translate(-50% , 50%)  scale(1);
          }
        50% , 75% {
            transform: translate(-50%, -30%) scale(0.5);
          }
        80%,  100% {
            transform: translate(-50%, -50%) scale(0);
          }
      }
  
</style>
