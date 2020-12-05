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
      fotos: [
        {
          url:
            "https://tabelacfop.com.br/assets/images/LogomarcaConectaTecnologia_v1.0-tts.png",
          title: "Conecta Tecnologia"
        },
        {
          url:
            "https://tabelacfop.com.br/assets/images/LogomarcaConectaTecnologia_v1.0-tts.png",
          title: "Conecta Tecnologia"
        }
      ]
    };
  }
};
</script>

<style>
</style>
