<template>
  <div>
    <layouts-header />
    <div class="container">
      <br />
      <Nuxt />
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
@import url("https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.0.2/css/bootstrap.min.css");
body
{
    height: 100%;
    min-height: 1400px;
    margin: 0;
    padding: 0;
    background-repeat: no-repeat;
    background-attachment: fixed;
       background: rgb(7,17,29);
background: -moz-linear-gradient(270deg, rgba(7,17,29,1) 0%, rgba(82,15,73,1) 48%, rgba(7,17,29,1) 100%);
background: -webkit-linear-gradient(270deg, rgba(7,17,29,1) 0%, rgba(82,15,73,1) 48%, rgba(7,17,29,1) 100%);
background: linear-gradient(270deg, rgba(7,17,29,1) 0%, rgba(82,15,73,1) 48%, rgba(7,17,29,1) 100%);
filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#07111d",endColorstr="#07111d",GradientType=1);  
}
</style>
