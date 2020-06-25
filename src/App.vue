<template>
  <div id="app">
    <v-app>
      <v-main>
        <v-container><application/></v-container>
      </v-main>
    </v-app>
  </div>
</template>

<script>
import application from './components/application'

export default {
  name: 'App',
  components: {
    application
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
