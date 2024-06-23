<template>
  <div class="visor">
    <div>
      <br />
      <img id="personagem" src="" alt="img aqui" />
    </div>

    <DadosApi />
  </div>
</template>




<script>
import DadosApi from "./Dados.vue";

export default {
  name: "VisorDisplay",

  components: {
    DadosApi,
  },
};
</script>

<style scoped>
div {
  width: 100%;
}

#personagem {
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  margin: 5% auto;
}
</style>