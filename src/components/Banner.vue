<template>
<div id="main-banner">
  <h1>Make Your Burguer</h1>
  <!-- <img src="@/assets/banner.jpg" alt="Banner Image" /> -->
</div>
</template>

<script>
export default {
name: 'Banner',
}
</script>

<style scoped>
#main-banner{
    background-image: url('/public/image/burger.jpg');
    background-repeat: no-repeat;
      background-size: cover;
      background-position: 0 -250px;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  
}

#main-banner h1 {
    color: #fff;
    font-size: 48px;
     text-align: center;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

</style>