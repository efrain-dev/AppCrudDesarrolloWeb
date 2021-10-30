<template>
  <Page class="page">
    <ActionBar class="action-bar">
      <GridLayout columns="50, *">
        <Label class="action-bar-title" text="Login" colSpan="2" />
      </GridLayout>
    </ActionBar>

    <!-- <GridLayout class="page__content">
            <Label class="page__content-icon fas" text.decode="&#xf015;"/>
            <Label class="page__content-placeholder" :text="message"/>
        </GridLayout> -->
    <StackLayout class="form">
      <StackLayout>
        <Image
          width="100"
          src="https://ps.w.org/login-customizer/assets/icon-128x128.png?rev=2455454"
        ></Image>
      </StackLayout>
      <StackLayout class="input-field">
        <TextField class="input" hint="Email" v-model="email"></TextField>
      </StackLayout>
      <StackLayout class="input-field">
        <TextField class="input" type="password" hint="Password" v-model="password"></TextField>
      </StackLayout>
      <Button
        text="Log In"
        class="btn btn-primary"
        @tap="onDrawerButtonTap()"
      ></Button>
    </StackLayout>
  </Page>
</template>

<script>
import * as utils from "~/shared/utils";
import { SelectedPageService } from "../shared/selected-page-service";
import Usuario from "./Usuario";
import axios from "axios/dist/axios";
import * as AppSettings  from '@nativescript/core/application-settings';

export default {
  data: function () {
    return {
      email: null,
      password:null,
    };
  },
  mounted() {
    SelectedPageService.getInstance().updateSelectedPage("Home");
  },
  computed: {
    message() {
      return "<!-- Page content goes here -->";
    },
  },
  
  methods: {
    onDrawerButtonTap() {
      axios({
        method: "POST",
        url: "https://apitest.online/api/login",
        data: {
          email: this.email,
          password: this.password,
        },
      }).then(
        (result) => {
            AppSettings.setString("token", result.data.access_token);
          this.$navigateTo(Usuario, {
            clearHistory: true,
          });
        },
        (error) => {
          alert('Datos incorrectos')
          console.error(error);
        }
      );
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
