<template>
  <div id="app">
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
          <imagem-responsiva
            v-meu-transform:scale.animate="1.2"
            :url="photo.url"
            :title="photo.titulo"
          ></imagem-responsiva>
          <meu-botao
            tipo="button"
            rotulo="REMOVER"
            @botaoAtivado="remove(photo)"
            :confirmacao="true"
            estilo="perigo"
          ></meu-botao>
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import ImagemResponsiva from "../shared/imagem-responsiva/imagem-responsiva.vue";
import Botao from "../shared/botao/Botao.vue";
import transform from "../../directives/Tranform";
export default {
  components: {
    "meu-painel": Painel,
    "imagem-responsiva": ImagemResponsiva,
    "meu-botao": Botao,
  },

  directives: {
    "meu-transform": transform,
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

  methods: {
    remove(photo) {
      alert("máh removendo oi - " + photo.titulo);
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
