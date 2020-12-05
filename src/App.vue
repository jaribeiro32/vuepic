<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <ul>
      <li v-for="foto of fotos">
        <img :src="foto.url" :alt="foto.title" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "VuePic",
      fotos: []
    };
  },
  created() {
    let promise = this.$http.get("http://localhost:3000/v1/fotos");

    promise
    .then(res => res.json())
    .then(fotos => (this.fotos = fotos), err => console.log(err));
  }
};
</script>

<style>
</style>
