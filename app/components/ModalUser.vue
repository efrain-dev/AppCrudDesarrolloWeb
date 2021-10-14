<template>
  <Page class="page container">
    <StackLayout orientation="vertical" class="container">
      <Label text="Nombre" horizontalAlignment="center" />
      <TextField placeholder="Nombre" v-model="name"></TextField>
      <Label text="Correo" horizontalAlignment="center" />
      <TextField placeholder="Correo" v-model="name"></TextField>
      <Label text="Telefono" horizontalAlignment="center" />
      <TextField placeholder="Telefono" v-model="name"></TextField>
      <Label text="Cuenta Github" horizontalAlignment="center" />
      <TextField placeholder="Cuenta Github" v-model="name"></TextField>
      <Label text="Foto" horizontalAlignment="center" />
      <TextField placeholder="Foto" v-model="name"></TextField>
      <Button @tap="saveUser" text="Guardar" class="btn-save" />
    </StackLayout>
  </Page>
</template>

<script>
export default {
  data: function () {
    return {
      name: "",
    };
  },
  mounted() {},
  computed: {},
  methods: {
    saveUser: function () {
      this.$modal.close();
    },
  },
};
</script>
<style>
.container {
  width: 1000px;
}
</style>