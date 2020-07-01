<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-light bg-light">
      <a href="#" class="navbar-brand">PAINEL COVID-19</a>
      <div class="navbar-nav mr-auto">
        <li class="nav-item">
          <a href="/pacientes" class="nav-link">Pacientes</a>
        </li>
        <li class="nav-item">
          <a href="/adicionar" class="nav-link">Adicionar Paciente</a>
        </li>
      </div>      
    </nav>
    <div class="container-fluid mt-3">
      <router-view />
    
    </div>

  </div>
  
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    //HelloWorld
  }
}
</script>

<style>
.navbar{
  box-shadow: 0px 5px 5px 5px black;
}
.nav-item a{
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 1.0rem;
  font-weight: 900;
}
</style>
