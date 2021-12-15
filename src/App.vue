<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

   <script>

    export default {
     name: 'app',
     components:{
     }
    }
   </script>

<style >

@supports(padding:max(0px)) {
    body, header, footer {
        padding-left: min(0vmin, env(safe-area-inset-left));
        padding-right: min(0vmin, env(safe-area-inset-right));
    }
}
body{
    background:#14181c;

}
html{
  /* min-height: calc(100% + env(safe-area-inset-top));
  padding: env(safe-area-inset-top) env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left); */
    min-height: calc(100% + env(safe-area-inset-top));
  padding: env(safe-area-inset-top) env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left);
  max-width: 600px;
  /* height: 100%; */
  box-sizing: border-box;
  margin: auto;
  text-align: center;
  /* border: 3px solid black; */
  background:#14181c;
  color: lightgray;
  font-family: Georgia, 'Times New Roman', Times, serif;
}

</style>
