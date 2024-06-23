<template>
  <div class="container">
    <header>
      <h1 class="titulo">API Rick and Morty</h1>
      <img
        width="128px;"
        height="128px;"
        src="./imgs/rick.png"
        alt=""
        srcset=""
      />
    </header>

    <br />

    <div class="pesquisa">
      <span>Pesquise aqui um personagem </span>

      <input
        type="number"
        placeholder="Número do personagem"
        name="pesquisa"
        id="pesquisa"
      />
      <input type="submit" v-on:click="click()" value="pesquisar" />
    </div>

    <VisorDisplay v-show="api" />
  </div>
</template>

<script>
import VisorDisplay from "./components/Visor.vue";

export default {
  name: "App",
  data() {
    return {
      api: "",
    };
  },
  components: {
    VisorDisplay,
  },

  methods: {
    click() {
      let pernsonagem = document.getElementById("pesquisa");

      fetch(`https://rickandmortyapi.com/api/character/${pernsonagem.value}`)
        .then((response) => {
          return response.json(); //pega a resposta da api e converte para json
        })
        .then((dataJson) => {
          // console.log(dataJson);  //imprime no console o json retornado
          this.SetApi(dataJson);
          this.api = true;
        })
        .catch((err) => {
          console.error("Erro ao consultar", err);
        });
    },
    SetApi(r) {
      let foto = document.getElementById("personagem");
      let nomeP = document.getElementsByClassName("nome")[0];

      foto.src = `${r["image"]}`;
      nomeP.innerHTML = `${r["name"]}`;

      if (r["name"] == "Rick Sanchez") {
        var texto = document.createTextNode(" The  Badass 😎");

        nomeP.appendChild(texto);
      }
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;

  padding-top: 5%;
}

header {
  display: flex;
  justify-content: center;
}

* {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

.titulo {
  width: 25%;
  text-align: center;
}

.pesquisa {
  margin: 0 auto;
  background: transparent;
}
.nome{
  color: rgb(0, 255, 0);
}
</style>
