<template>
  <button
    class="ui inverted pink button"
    data-tooltip="Abrirá um form para edição"
    data-position="bottom left"
  >
    Editar Gif
  </button>
</template>

<script>
export default {
  props: ["informacoesGif","dadosEditados"],
  data() {
    return {
      configFetch: {
        method: "put",
        headers: {
          "Content-Type:": "application/json",
        },
      },
    };
  },
  methods: {
    editarGif(dadosEditados) {
      this.configFetch.body = {
        gif: {
          nome: dadosEditados.title,
          id: this.informacoesGif.id,
          url: this.informacoesGif.url,
          user: dadosEditados.user,
        },
      };
      fetch(
        `https://simulandoedicao/gif/${this.configFetch.body.gif.id}`,
        JSON.stringify(this.configFetch)
      )
        .then((response) => response.json())
        .then((data) => console.log(data));
    },
  },
};
</script>

<style>
</style>