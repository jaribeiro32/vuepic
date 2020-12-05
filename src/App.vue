<template>
  <div id="app" class="body">
    <h1 class="title">{{ title }}</h1>
    <ul class="photos-list">
      <li class="photos-item" v-for="photo of photos">
        <img :src="photo.url" :alt="photo.title" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "VuePic",
      photos: []
    };
  },
  created() {
    let promise = this.$http.get("http://localhost:3000/v1/fotos");

    promise
    .then(res => res.json())
    .then(photos => (this.photos = photos), err => console.log(err));
  }
};
</script>

<style>
.body{
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}
.title{
  text-align: center;
}

.photos-list{
  list-style: none;
}

.photos-list .photos-item{
display: inline-block;
}

</style>
