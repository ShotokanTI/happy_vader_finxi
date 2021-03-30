<template>
  <div
    class="container-inf"
    style="background:rgba(0, 0, 0, 0.9); width: 98%; position: absolute;padding:10px;margin:5px"
  >
    <p>
      Dimensões: {{ gifData.images.original.width }} x
      {{ gifData.images.original.height }} px
    </p>
    <p class="column-1">
      Tamanho arquivo:
      {{ converterTamanho(gifData.images.original.size, true) }}
    </p>
    <p class="column-1">
       Frames: {{gifData.images.original.frames}} 
    </p>
    <p class="uploaded-row">
        Uploaded:{{gifData.import_datetime}}
    </p>
    <p class="rating-row">
      Rating: {{ gifData.rating.toUpperCase() }}
    </p>
    <div style="display:flex;">
    <p>Nome Gif: {{gifData.title}}</p>
    <input v-if="false" :value="gifData.title" style="width:89px;height:20px;outline:none" type="text">
    </div>
    <p>Id Gif: {{gifData.id}}</p>
    </div>
</template>

<script>
export default {
  props: ["gifData"],
  methods: {
    converterTamanho(bytes, si = false, dp = 1) {
      const thresh = si ? 1000 : 1024;

      if (Math.abs(bytes) < thresh) {
        return bytes + " B";
      }

      const units = ["kB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB"];
      let u = -1;
      const r = 10 ** dp;

      do {
        bytes /= thresh;
        ++u;
      } while (
        Math.round(Math.abs(bytes) * r) / r >= thresh &&
        u < units.length - 1
      );

      return bytes.toFixed(dp) + " " + units[u];
    },
  },
};
</script>

<style>
p {
  font-size: 11px;
  color: white;
  font-family: Arial, Helvetica, sans-serif;
}
.container-inf {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.column-1{
    grid-column-start: 1;
}
.uploaded-row{
    grid-column-start:2;
    grid-row-start: 1;
}
.rating-row{
    grid-column-start: 2;
    grid-row-start:2;
}
</style>