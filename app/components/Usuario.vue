<template>
  <Page class="page">
    <ActionBar class="action-bar">
      <GridLayout columns="50, *">
        <Label class="action-bar-title" text="Usuario" colSpan="2" />
        <Button
          text="Crear Usuario"
          @tap="onButtonTap"
          class="btn-save"
          colSpan="3"
        />
      </GridLayout>
    </ActionBar>

    <GridLayout class="page__content">
      <ListView for="item in listOfItems">
        <v-template>
          <DockLayout>
            <Label :text="item.name" dock="left" width="120" />
            <Label :text="item.email" dock="left" width="120" />

            <Button
              text="Editar"
              dock="left"
              width="60"
              class="btn-edit"
              @tap="editUser(item)"
            />
            <Button
              text="Eliminar"
              dock="left"
              width="60"
              class="btn-delete"
              @tap="deleteUser(item)"
            />
          </DockLayout>
        </v-template>
      </ListView>
    </GridLayout>
  </Page>
</template>

<script>
import * as utils from "~/shared/utils";
import { SelectedPageService } from "../shared/selected-page-service";
import ModalUser from "./ModalUser";
import * as AppSettings from "@nativescript/core/application-settings";

import axios from "axios/dist/axios";
export default {
  data: function () {
    return {
      listOfItems: [],
    };
  },
  mounted() {
    SelectedPageService.getInstance().updateSelectedPage("Usuario");
    this.getData();
  },
  computed: {},
  methods: {
    onDrawerButtonTap() {
      utils.showDrawer();
    },
    created() {
      this.interval = setInterval(() => this.getData(), 10000);
    },
    onButtonTap() {
      this.$showModal(ModalUser, {
        props: {
          dataClient: {
            id_cliente: null,
            name: null,
            email: null,
            github: null,
            profile_photo_path: null,
          },
        },
      });
      this.getData();
    },
    editUser(item) {
      this.$showModal(ModalUser, { props: { dataClient: item } });
      this.getData();
    },
    deleteUser(item) {
      confirm({
        title: "Confirmar",
        message: "¿Estas seguro que deseas elminar el usuario?",
        okButtonText: "Si, Eliminalo",
        cancelButtonText: "No, Cancelar",
      }).then((result) => {
        if (result) {
          axios({
            method: "DELETE",
            url: "https://apitest.online/api/clientes/"+item.id_cliente,
            headers: {
              Authorization: "Bearer " + AppSettings.getString("token"),
            },
          }).then(
            (result) => {
               alert("Eliminado Con exito");
                     this.getData();

            },
            (error) => {
              alert(error);
            }
          );
        }
      });
    },
    getData() {
      axios({
        method: "GET",
        url: "https://apitest.online/api/clientes",
        headers: {
          Authorization: "Bearer " + AppSettings.getString("token"),
        },
      }).then(
        (result) => {
          this.listOfItems = result.data;
        },
        (error) => {
          console.error(error);
        }
      );
    },
  },
};
</script>

<style  lang="scss">
// Start custom common variables
@import "@nativescript/theme/scss/variables/blue";

// End custom common variables

// Custom styles
.btn-edit {
  background: yellow;
  color: black;
}
.btn-save {
  background: green;
  color: white;
}
.btn-delete {
  background: red;
  color: white;
}
</style>
