<template>
    <div class="head">
        <h1>{{greeting}}</h1>
    </div>
</template>

<script>
export default {
    data(){
        return {
            greeting: 'hello',
        }
    }
}
</script>

<style scoped>
.head{
background-color:#ffc90f;
height:100%;
/* width:100vw;
padding:0;
margin:0;
box-sizing: border-box; */
}

/* header{
  width:100%;
  height:80;
  color:#d32228;
}

.header {
  display:inline-block;
  text-align:center;
    background-color:#ffc90f;

}

.header img {
  float:left;
  margin-left: 20px;
  margin-top:23px;
} */
</style>