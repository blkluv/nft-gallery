<template>
  <b-navbar
    fixed-top
    shadow
    spaced
    wrapper-class="container"
    style="background-color: #000000;box-shadow:unset"
    :close-on-click="false"
  >
    <template #brand>
      <b-navbar-item tag="router-link" :to="{ path: '/' }">
        <img
          src="@/assets/logo.png"
          alt="First NFT market explorer on Kusama and Polkadot"
        />
      </b-navbar-item>
    </template>
    <template #start class="start">
      <b-navbar-item
        class="nav-item-text"
        tag="router-link"
        :to="{ name: 'rmrk' }"
      >
        <strong>{{ $t("Create") }}</strong>
      </b-navbar-item>
      <b-navbar-item tag="router-link" :to="{ name: 'nft' }" class="nav-item-text">
        <strong>{{ $t("Gallery") }}</strong>
      </b-navbar-item>
      <b-navbar-dropdown arrowless collapsible label="Extra" class="nav-item-text">
        <b-navbar-item tag="router-link" :to="{ name: 'rmrkCredit' }">
          {{ $t("Credit") }}
        </b-navbar-item>
        <b-navbar-item tag="router-link" :to="{ name: 'settings' }">
          {{ $t("Settings") }}
        </b-navbar-item>
      </b-navbar-dropdown>
    </template>
    <template #end>
      <b-navbar-item> 
        <div class="buttons">
          <b-field grouped>
            <b-button tag="router-link" :to="{ name: 'rmrkFaq' }">
              F.A.Q.
            </b-button>
            <LocaleChanger />
            <b-button
              tag="a"
              type="is-info"
              outlined
              href="https://twitter.com/luvnft"
            >
              <b-icon pack="fab" icon="twitter"> </b-icon>
              <strong>LUV NFT</strong>
            </b-button>
          </b-field>
        </div>
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import LocaleChanger from "@/components/shared/SwitchLocale.vue";
import { getCurrentColor } from "@/colors";
import i18n from "@/i18n.ts";

@Component({
  components: {
    LocaleChanger,
  },
})
export default class NavbarMenu extends Vue {
  private color: string = getCurrentColor();
  public navbar: any = [
    {
      name: i18n.t("Create"),
      tag: "router-link",
      to: { name: "rmrk" },
      strong: true,
    },
    {
      name: i18n.t("Gallery"),
      tag: "router-link",
      to: { name: "nft" },
      strong: true,
    },
  ];
  public navbarExtra: any = [
    {
      name: i18n.t("Accounts"),
      icon: "users",
      to: { name: "accounts" },
      tag: "router-link",
    },
    {
      name: i18n.t("Credit"),
      icon: "users",
      to: { name: "rmrkCredit" },
      tag: "router-link",
      strong: true,
    },
    {
      name: i18n.t("Transfer"),
      icon: "paper-plane",
      to: { name: "transfer" },
      tag: "router-link",
    },
    {
      name: i18n.t("Settings"),
      icon: "cogs",
      tag: "router-link",
      to: { name: "settings" },
    },
  ];
  private navbarExternal: any = [
    {
      name: "Twitter",
      tag: "a",
      href: "https://twitter.com/luvnft",
    },
  ];

  // get chainColor() {
  //   return {
  //     'border-bottom': `4px ${this.color} solid`
  //   }
  // }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Archivo&family=Chivo:ital,wght@1,900&display=swap');
.nav-item-text {
  color: white !important;
  font-size: 44px;
  font-family: 'Archivo', sans-serif !important;
}
.start {
 font-family: 'Archivo', sans-serif !important;
}
.nav-item-text a {
  color: white;
  font-size: 44px;
  font-weight: bold;
}
a:hover {
  color: black !important;
}
.navbar-dropdown {
  background-color: black;
}
</style>
