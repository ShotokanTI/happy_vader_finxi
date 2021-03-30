<template>
  <div style="position:fixed;z-index:10;width: 80%" class="container-pesquisa">
    <div style="margin: 20px; width: 80%" class="ui massive icon input ui buttons">
      <input type="text" placeholder="Procure um gif aqui" v-model="buscaGif" />
      <button
        style="border: 0px; background-color: #f9636e; cursor: pointer"
        @click="
          procurarGif();
          resetarScroll();
          habilitarReq = true;
        "
      >
        <img
          width="50px"
          style="border-radius: 99px; margin-top: 25px; border: 0px"
          src="https://cdn.drawception.com/images/panels/2015/6-26/DqBsZ671AH-2.png"
          alt=""
        />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      buscaGif: "Jar Jar Binks",
      api_key: "vX0AQqjgDxL2ICDQKSFBTBEJK9z2p5GU",
      gif: [],
      habilitarReq: true,
      happyvader: false,
    };
  },
  mounted() {
    this.procurarGif();
    this.detectarFimScroll();
  },
  methods: {
    relatedGifs() {
      if (this.habilitarReq) {
        fetch(
          `https://api.giphy.com/v1/gifs/search?q=${this.buscaGif}&offset=${this.offsetGif}&type=gifs&sort=&api_key=${this.api_key}`,
          { method: "GET", mode: "cors" }
        )
          .then((promisse) => promisse.json())
          .then((gifObject) => {
            this.gif = this.gif.concat(gifObject.data);
            this.$emit("enviarGifParent", this.gif);
            this.offsetGif += gifObject.data.length;
            if (gifObject.data == "") {
              this.habilitarReq = false;
            }
          });
      }
    },
resetarScroll() {
      window.scrollTo(0, 0);
    },
    detectarFimScroll() {
      window.onscroll = () => {
        if (window.scrollY + window.outerHeight > document.body.scrollHeight) {
          this.relatedGifs();
        }
      };
    },

    procurarGif() {
      fetch(
        `https://api.giphy.com/v1/gifs/search?q=${this.buscaGif}&api_key=${this.api_key}`,
        { method: "GET", mode: "cors" }
      )
        .then((promisse) => promisse.json())
        .then((gifObject) => {
          this.gif = gifObject.data;
          this.offsetGif = gifObject.data.length;
          this.$emit("enviarGifParent", this.gif);
        });
    },
  },
};
</script>

<style>
</style>