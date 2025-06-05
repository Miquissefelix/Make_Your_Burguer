<template>
  <footer id="footer">
    <p>Make Your Burguer &copy; 2025</p>
  </footer>
</template>

<script>
export default {
    name: 'Footer'

}
</script>

<style scoped>
#footer {
  background-color: #222;
  color: #fcba03;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  position: fixed;
  left: 0;
  bottom:0 ;
 height: 50px;
 z-index: 100;
}

</style>