<template>
  <div style="padding-top: 140px" class="ui grid centered">
    <div
      style="border-bottom: 1px solid #f9636e"
      class="five wide column row"
      v-for="(gifs, index) in gifs"
      :key="index"
    >
      <img
        @click="
          informacoesGif(gifs);
          resetarScroll();
          gifsSalvos(gifs,index);
        "
        style="border-radius: 4px; padding-left: 10px; cursor: pointer"
        width="100%"
        :max-height="gifs.images.fixed_width.height"
        :src="gifs.images.fixed_width.url"
        alt=""
      />
    </div>
  </div>
</template>

<script>
export default {
  props: ["gifs"],
  data(){
    return{
      count:0
    }
  },
  methods: {
    gifsSalvos(gifs,index){
      let gifClicked = {
        config:{[gifs.id]:false},
        i:index
      }
      this.$emit('gifClicked',gifClicked)
    },
    informacoesGif(infGif) {
      this.$emit("infGif", infGif);
    },
    resetarScroll() {
      window.scrollTo(0, 0);
    },
  },
};
</script>
<style>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
