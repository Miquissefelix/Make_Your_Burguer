<template>
  <div class="message-container">
     <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
 name: 'Message',
 props:{
    msg:String
 }
}
</script>

<style scoped>
.message-container {
  background-color: #cce5ff;
  color: #004085;
  border: 2px solid #b8daff;
  padding: 10px;
  border-radius: 5px;
  max-width: 400px;
  margin: 30px auto;
  text-align: center;
}

</style>