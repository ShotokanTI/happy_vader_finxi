<template>
  <div id="app">
    <div
      style="position: relative"
      class="ui grid two column container stackable"
    >
      <div style="width: 100vw" class="row">
        <ContainerPesquisa @enviarGifParent="getGifParent" />
      </div>
      <div style="position: relative" class="left floated column centered">
        <div
          style="
            margin-top: 108px;
            display: flex;
            flex-direction: column;
            justify-content: center;
          "
          v-if="gifData"
        >
          <div style="display: flex; justify-items: center">
            <p style="font-size: 14px; color: gray">{{ gifData.title }}</p>
            <img
              @click="informacoes = !informacoes"
              style="background: pink; margin-left: 10px; cursor: pointer"
              width="30px"
              height="17px"
              src="../src/assets/icons/ellipsis-h-solid.svg"
              alt=""
            />
          </div>
          <div class="ui horizontal">
            <div style="position: relative; max-width: 480px; height: 300px">
              <div
                style="
                  position: absolute;
                  background-color: #15120e;
                  width: 100%;
                "
                class=""
              >
                <InformacoesGif v-if="informacoes" :gifData="gifData" />
              </div>
              <img
                style="border-radius: 4px"
                width="100%"
                height="100%"
                :src="gifData.images.original.webp"
                alt=""
              />
            </div>
            <div
              style="padding-top: 20px; flex-wrap: no-wrap"
              class="ui buttons"
            >
              <salvar-button
                @click.native="estadoButton(true)"
                :informacoesGif="gifData"
              />
              <editar-button
                @click.native="abrirModalEdit"
                ref="editar"
                :informacoesGif="gifData"
                :dadosEditados="informacoesAlteradas"
                v-if="gifsClickedAndSaved[indexAtual][gifData.id]"
              />
              <excluir-button
                @click.native="estadoButton(false)"
                v-if="gifsClickedAndSaved[indexAtual][gifData.id]"
                :idGif="gifData.id"
              />
            </div>
          </div>
        </div>
      </div>
      <div style="margin-top: 140px" class="right floated column">
        <ListarGifs @gifClicked="statusGif" @infGif="infGif" :gifs="gif" />
      </div>
    </div>
    <modal-edit @dadosAlterados="getDadosAlterados" :gifModal="gifData" />
  </div>
</template>

<script>
import ContainerPesquisa from "./components/ContainerPesquisa.vue";
import EditarButton from "./components/EditarButton.vue";
import ExcluirButton from "./components/ExcluirButton.vue";
import InformacoesGif from "./components/InformacoesGif.vue";
import ModalEdit from './components/modalEdit.vue';
import SalvarButton from "./components/SalvarButton.vue";
import ListarGifs from "./pages/main/ListarGifs.vue";

export default {
  name: "App",
  components: {
    ListarGifs,
    InformacoesGif,
    ContainerPesquisa,
    SalvarButton,
    EditarButton,
    ExcluirButton,
    ModalEdit,
  },

  data() {
    return {
      informacoes: false,
      gifData: "",
      gif: [],
      offsetGif: 0,
      gifsClickedAndSaved: [],
      compareArray: [],
      gifIdenti: false,
      indexAtual: 0,
      habilitarReq: true,
      informacoesAlteradas:''
    };
  },
  methods: {
    getDadosAlterados(payload){
      // this.informacoesAlteradas = payload
      this.$refs.editar.editarGif(payload)
    },
    abrirModalEdit(){
      $('.ui.modal').modal('show')
    },
    estadoButton(status) {
      let converted = JSON.parse(JSON.stringify(this.gifsClickedAndSaved));
      for (let i in converted) {
        if (Object.keys(converted[i]).toString() === this.gifIdenti) {
          this.gifsClickedAndSaved[i][this.gifIdenti] = status;
        }
      }
    },
    verificaSeFoiSalvo() {
      let converted = JSON.parse(JSON.stringify(this.gifsClickedAndSaved));
      for (let i in converted) {
        if (Object.keys(converted[i]).toString() === this.gifIdenti) {
          this.indexAtual = i;
        }
      }
    },
    statusGif(payload) {
      if (
        this.compareArray.indexOf(Object.keys(payload.config).toString()) === -1
      ) {
        this.gifsClickedAndSaved.push(payload.config);
      }
      this.gifIdenti = Object.keys(payload.config).toString();
      this.compareArray.push(Object.keys(payload.config).toString());

      this.verificaSeFoiSalvo();
    },
    getGifParent(payload) {
      this.gif = payload;
    },
    infGif(payload) {
      this.gifData = payload;
    },
    isIdEqual(existente, novo) {
      if (existente.id !== novo.id) {
        return novo;
      }
    },
  },
};
</script>

<style>
span {
  color: white;
}
.verdadeirovilao {
  width: 100%;
  opacity: 0.05;
  border-radius: 9999px;
}
.matar-vader-de-rir {
  width: 100%;
  display: flex;
  flex-direction: column;
  bottom: 0;
  position: absolute !important;
}
.content-jarjar {
  max-width: 400px;
  position: relative;
}
.input-pesquisa {
  position: sticky !important;
  z-index: 10;
  background-color: #121212;
  margin-top: 10px;
}
</style>
