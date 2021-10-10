<template>
    <Navbar :logo="logo_src" :alt="app_name"/>
    <router-view/>
    <Footer/>
</template>


<script>

import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'


export default {
  components:{
    Navbar,
    Footer,
  },
  data(){
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burger"
    }
  }
}
</script>


<style>

  :root{
    --primary-color: #222;
    --secundary-color: #fcba03;;
    --border-color: #111;
  }

  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }


  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: var(--primary-color);
    border-radius: 0px 0px 100px 0px;
  }

</style>>


