<template>
    <div id="nav">
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt"  id="logo">
    </router-link>
    <router-link to="/">Home</router-link> 
    <router-link to="/pedidos">Pedidos</router-link>
    <router-link to="/contato">Contatos</router-link>
  </div>
</template>


<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"]
}
</script>


<style scoped>
    #nav {
        background-color: var(--primary-color);
        border-bottom: 4px solid var(--border-color);
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

      #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }

   #logo {
        widows: 40px;
        height: 40px;
    }

    #nav a {
        color: var(--secundary-color);
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }


    #nav a:hover{
        color: #fff;
        
    }
</style>

