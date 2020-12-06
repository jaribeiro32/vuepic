<template>
  <div id="app" class="body">
    <h1 class="title">{{ title }}</h1>
    <input
      type="search"
      name="search"
      class="filtro"
      v-on:input="filtro = $event.target.value"
      placeholder="filtre pelo titulo"
    />
    <ul class="photos-list">
      <li class="photos-item" v-for="photo of fotosComFiltro">
        <meu-painel :title="photo.titulo">
          <img class="imagem-responsiva" :src="photo.url" :alt="photo.titulo" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "./components/shared/painel/Painel.vue";
export default {
  components: {
    "meu-painel": Painel,
  },
  data() {
    return {
      title: "VuePic",
      photos: [],
      filtro: "",
    };
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        /* filtrar */
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.photos.filter((photo) => exp.test(photo.titulo));
      } else {
        return this.photos;
      }
    },
  },
  created() {
    let promise = this.$http.get("http://localhost:3000/v1/fotos");

    promise
      .then((res) => res.json())
      .then(
        (photos) => (this.photos = photos),
        (err) => console.log(err)
      );
  },
};
</script>

<style>
.body {
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}
.title {
  text-align: center;
}

.photos-list {
  list-style: none;
}

.photos-list .photos-item {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
