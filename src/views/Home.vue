<template>
  <div id="app" class="container">
<h1>{{name}}</h1>
  </div>
</template>

<script>
export default {
  name: "Home",
  mounted() {
    console.log("mounted");
    this.$nextTick(() => {
      // Fires before full page is rendered
    });
  },
  data() {
    return {
      name:'vue-pwa-template',
    };
  },
  methods: {
    
  },
  created: function () {},
};
</script>

<style scoped>
.container {
  display: grid;
  grid-template-columns: 100%;
  grid-template-rows: 80px auto 50px;
}

.day {
  min-height: 4rem;
}

b.date {
text-align: right;
}

span.dayrecipe {
  text-align: right;
}

.item {
  /* border:1px solid black; */
}
/* img {
  display: block;
  margin: auto;
  width: 20rem;
} */



li {
  list-style-type:none;
}

form {
  margin-top: 1rem;
}

input {
  width: 70%;
  height: 2rem;
  margin-top: 0.5rem;
  margin-bottom: 1rem;
}

ul {
  padding-top: 1rem;
  font-size: 1.5rem;
  text-align: left;
}

ul > li:nth-child(even) {
  color: grey;
}

ul button {
  margin: 0 10px;
}

ul a {
  margin: 0 10px;
}

ul a:hover {
  /* display:none; */
}

.header {
  grid-row: 1;
  align-self: top;
}
</style>
