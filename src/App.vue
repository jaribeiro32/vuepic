<template>
  <div id="app" class="body">
    <h1 class="title">{{ title }}</h1>
    <ul class="photos-list">
      <li class="photos-item" v-for="photo of photos">
        <div class="painel">
          <h2 class="painel-title">{{ photo.titulo }}</h2>
          <div class="painel-content">
            <img class="imagem-responsiva" :src="photo.url" :alt="photo.titulo" />
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "VuePic",
      photos: [],
    };
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

 /* estilo do painel */

   .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-title {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }

  .imagem-responsiva{
    width: 100%;
  }
</style>
