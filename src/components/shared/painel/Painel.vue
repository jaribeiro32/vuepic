<template>
  <div class="painel">
    <h2 class="painel-title" @dblclick="visivel = !visivel">{{ title }}</h2>
    <transition name="painel-fade">
      <div class="painel-content" v-show="visivel">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["title"],

  data() {
    return {
      visivel: true,
    };
  },
};
</script>

<style scoped>
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

.painel-fade-enter,
.painel-fade-leave-active {
  opacity: 0;
}

.painel-fade-enter-active,
.painel-fade-leave-active {
  transition: opacity 0.4s;
}

.painel-content{
  overflow: hidden;
}


</style>
