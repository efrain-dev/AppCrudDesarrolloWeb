<template>
  <Page class="page">
    <ActionBar class="action-bar">
      <NavigationButton visibility="hidden" />
      <GridLayout columns="50, *">
        <Label class="action-bar-title" text="Usuario" colSpan="2" />
        <Label class="fas" text.decode="&#xf0c9;" @tap="onDrawerButtonTap" />
        <Button text="Button" @tap="onButtonTap" />
      </GridLayout>
    </ActionBar>

    <GridLayout class="page__content">
      <ListView for="item in listOfItems" @itemTap="onItemTap">
        <v-template>
          <Label :text="item" />
        </v-template>
      </ListView>
    </GridLayout>
  </Page>
</template>

<script>
import * as utils from "~/shared/utils";
import { SelectedPageService } from "../shared/selected-page-service";
import {
  ModalDialogService,
  ModalDialogOptions,
} from "nativescript-angular/modal-dialog";

export default {
  data: function () {
    return {
      listOfItems: ["Fernado", "Rodrigo", "Roberto"],
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
      var dialogs = require("tns-core-modules/ui/dialogs");
      dialogs
        .action("Your message", "Cancel button text", ["Option1", "Option2"])
        .then(function (result) {
          console.log("Dialog result: " + result);
          if (result == "Options1") {
            //Do action1
          } else if (result == "Option2") {
            //Do action2
          }
        });
    },
  },
};
</script>

<style scoped lang="scss">
// Start custom common variables
@import "@nativescript/theme/scss/variables/blue";
// End custom common variables

// Custom styles
</style>
