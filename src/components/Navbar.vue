<template>
   <header>
   
    <div >
      <nav id="nav">
        <router-link to="/" id="logo-url"><img :src="logo" :alt="alt"  id="logo"/></router-link>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/pedidos">Pedidos</RouterLink>
      </nav>
    </div>
  </header>

</template>

<script>
export default {
    name: 'Navbar',
    props:["logo","alt"]

}
</script>

<style scoped>
#nav{
  background-color: #222;
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  /* position: fixed;
  z-index: 100; */
  width: 100%;
}
#nav #logo-url{
 margin: auto;
 margin-left: 0;
}
#logo {
  height: 40px;
  width: 40px;
}
#nav a{
  color: #fcba03;
  text-decoration: none;
  margin: 12px;
  transition: .5s;
  
}
#nav a:hover{
  color: #fff;
}
</style>