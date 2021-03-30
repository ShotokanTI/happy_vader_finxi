<template>
  <button
    @click="deletarGif"
    class="ui inverted red button"
    data-tooltip="Exclua seus gifs em um banco externo,é só clicar =)"
    data-position="bottom right"
  >
    Excluir Gif
  </button>
</template>

<script>
export default {
  props: ["idGif"],
  data() {
    return {
      configFetch: {
        method: "delete",
        headers: {
          "Content-Type:": "application/json",
        },
      },
    };
  },
  methods: {
      deletarGif() {
          this.configFetch.gif_id = this.idGif
      fetch(`https://simulandodelete/gif/${this.idGif}`, this.configFetch)
        .then((response) => response.json())
        .then((data) => console.log(data));
    },
  },
};
</script>

<style>
</style>