<template>
  <Page class="page container">
    <StackLayout orientation="vertical" class="container">
      <Label text="Nombre" horizontalAlignment="center" />
      <TextField placeholder="Nombre" v-model="name"></TextField>
      <Label text="Correo" horizontalAlignment="center" />
      <TextField placeholder="Correo" v-model="email"></TextField>
      <Label text="Cuenta Github" horizontalAlignment="center" />
      <TextField placeholder="Cuenta Github" v-model="github"></TextField>
      <Label text="Foto" horizontalAlignment="center" />
      <TextField placeholder="Foto" v-model="profile_photo_path"></TextField>
      <Button @tap="saveUser" text="Guardar" class="btn-save" />
    </StackLayout>
  </Page>
</template>

<script>
import * as AppSettings from "@nativescript/core/application-settings";
import axios from "axios/dist/axios";

export default {
  props: ["dataClient"],
  
  data: function () {
    return {
      id_cliente:this.dataClient.id_cliente,
      name: this.dataClient.name,
      email: this.dataClient.email,
      github: this.dataClient.github,
      profile_photo_path: this.dataClient.profile_photo_path,
    };
  },
  mounted() {
    console.log(this.dataClient);
  },
  computed: {},
  methods: {
    saveUser: function () {
        let dataSend = {
            id_cliente:this.id_cliente,
            name: this.name,
            email: this.email,
            github: this.github,
            profile_photo_path: this.profile_photo_path,
          }
        axios({
          method: "POST",
          url: "https://apitest.online/api/clientes",
          data: dataSend,
          headers: {
            Authorization: "Bearer " + AppSettings.getString("token"),
          },
        }).then(
          (result) => {
            alert("Guardado con exito")
            this.$modal.close();;

          },
          (error) => {
            alert(error)
          }
        );

      

      
    },
  },
};
</script>
<style>
.container {
  width: 1000px;
}
</style>