<template>
  <Page class="page">
    <ActionBar class="action-bar">
      <NavigationButton visibility="hidden" />
      <GridLayout columns="50, *">
        <Label class="action-bar-title" text="Usuario" colSpan="2" />
        <Label class="fas" text.decode="&#xf0c9;" @tap="onDrawerButtonTap" />
      </GridLayout>
    </ActionBar>

    <GridLayout class="page__content">
      <Button text="Crear" @tap="onButtonTap" class="btn-save"  />

      <ListView for="item in listOfItems">
        <v-template>
          <DockLayout>
            <Label :text="item" dock="left" width="240" />
            <Button
              text="Editar"
              dock="left"
              width="60"
              class="btn-edit"
              @tap="editUser"
            />
            <Button text="Eliminar" dock="left" width="60" class="btn-delete"  @tap="deleteUser"/>
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
export default {
  data: function () {
    return {
      listOfItems: ["Fernado Martinez", "Rodrigo Alvarez", "Roberto Gomez"],
    };
  },
  mounted() {
    SelectedPageService.getInstance().updateSelectedPage("Usuario");
  },
  computed: {},
  methods: {
    onDrawerButtonTap() {
      utils.showDrawer();
    },

    onButtonTap() {
      this.$showModal(ModalUser);
    },
    editUser() {
      this.$showModal(ModalUser);

    },
    deleteUser() {
      confirm({
        title: "Confirmar",
        message: "¿Estas seguro que deseas elminar el usuario?",
        okButtonText: "Si, Eliminalo",
        cancelButtonText: "No, Cancelar",
      }).then((result) => {
        if (result) {
          alert("Eliminado Con exito");
        }
      });
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
