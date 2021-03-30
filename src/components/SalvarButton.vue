<template>
  <button
    @click="salvarGif"
    class="ui inverted green button"
    data-tooltip="Salve seus gifs,Darth vader vai adorar! hahah"
    data-position="bottom left"
  >
    Salvar Gif
  </button>
</template>

<script>
export default {
  props: ["informacoesGif"],
  data() {
    return {
      configFetch: {
        method: "post",
        headers: {
          "Content-Type:": "application/json",
        },
      },
    };
  },
  methods: {
    salvarGif() {
      this.configFetch.body = JSON.stringify({
        gif: {
          nome: this.informacoesGif.title,
          id: this.informacoesGif.id,
          url: this.informacoesGif.url,
          user: this.informacoesGif.user,
        },
      });
      fetch("https://simulandoinsercao/", this.configFetch)
        .then((response) => response.json())
        .then((data) => console.log(data));
    },
  },
};
</script>

<style>
button {
  width: min(120px, 32vw);
}
</style>