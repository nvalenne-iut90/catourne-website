<template>
  <div id="app">
    <!--<NavBar/>-->
    <router-view/>
  </div>
</template>

<script>

//import NavBar from "@/components/NavBar.vue";

export default {
  name: 'App',
  //components: {NavBar},

  data: () => ({
    //
  }),
};
</script>

<style>
  #app {
    color: white;
    font-family: "Press Start 2P", "sans-serif";
    display: flex;
    flex-flow: column wrap;
    width: 100%;
  }
  body {
    max-width: 100%;
    margin: 0;
    overflow-x: hidden;
  }
  html {
    background: #030304;
    animation-name: party_mode;
    animation-duration: 1s;
    animation-iteration-count: infinite;
  }
  /*
  @keyframes party_mode {
    0%   {background: red;}
    25%  {background: yellow;}
    50%  {background: blue;}
    100% {background: green;}
  }
   */


</style>
