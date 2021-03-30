<template>
  <div class="ui modal">
    <i class="close icon"></i>
    <div class="header">Edição de gif</div>
    <div style="width: 100%" class="image content">
      <form style="width:100%" action="" id="editGif">
        <div class="container-form">
          <div class="ui input">
            <div class="content-column ui input">
              <label for="nome">Nome Gif</label>
              <input
                :value="gifModal.title"
                type="text"
                name="nome"
                id="nome"
              />
            </div>
          </div>
          <div class="ui input">
            <div class="content-column ui input">
              <label for="description">Descricao Gif</label>
              <input
                :value="gifModal.user.description"
                type="text"
                name="description"
                id="description"
              />
            </div>
          </div>
          <div class="ui input">
            <div class="content-column ui input">
              <label for="Source">Origem Gif</label>
              <input
                :value="gifModal.user.display_name"
                type="text"
                name="displayname"
                id="Source"
              />
            </div>
          </div>
          <div class="ui input">
            <div class="content-column ui input">
              <label for="UsernameGif">Username Gif</label>
              <input
                :value="gifModal.user.username"
                name="username"
                type="text"
                id="UsernameGif"
              />
            </div>
          </div>
        </div>
      </form>
    </div>
    <div class="actions">
      <div class="ui black deny button">Cancelar</div>
      <div @click="editGif" class="ui positive right labeled icon button">
        Salvar edição
        <i class="checkmark icon"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["gifModal"],
  data() {
    return {
      formData: [],
    };
  },
  methods: {
    editGif() {
      let gifName = document.getElementById("editGif");
      let form = new FormData(gifName);
      let gifEditado = {
        title: form.get("nome"),
        user: {
          username: form.get("username"),
          description: form.get("description"),
          display_name: form.get("displayname"),
        },
      };
      this.$emit("dadosAlterados", gifEditado);
    },
  },
};
</script>

<style>
.container-form {
  --auto-grid-min-size: 16rem;
  display: grid;
  grid-template-columns: repeat(
    auto-fill,
    minmax(var(--auto-grid-min-size), 1fr)
  );
  grid-gap: 1rem;
  justify-items: center;
}
label {
  padding-right: 10px;
  font-size: 15px;
}
.content-column ui input {
  display: flex;
  flex-direction: column;
}
</style>