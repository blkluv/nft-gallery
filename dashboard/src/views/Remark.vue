<template>
  <div class="columns">
    <div class="column is-7 is-offset-3">
      <section>
        <br />
        <b-tabs type="is-toggle" v-model="activeTab" destroy-on-hide expanded>
          <b-tab-item
            v-for="x in components"
            :key="x"
            :label="x"
            class="custom-tabs"
          >
            <component v-bind:is="x"></component>
          </b-tab-item>
        </b-tabs>
      </section>
    </div>
  </div>
</template>

<script lang="ts" >
import { Component, Vue } from "vue-property-decorator";
const Collection = () => import("@/components/rmrk/Create/Create.vue");
const NFT = () => import("@/components/rmrk/Create/CreateToken.vue");

const components = { Collection, NFT };

@Component({ components })
export default class Remark extends Vue {
  public activeTab: number = 0;
  public components: string[] = ["Collection", "NFT"];
}
</script>
<style>
.tabs.is-toggle li.is-active a {
  background-color: #beef00 !important;
  border-color: #beef00 !important;
  color: #000 !important;
  font-family: 'Archivo', sans-serif !important;
}
.tabs.is-toggle li a{
  background-color: white;
}
.b-tabs .tab-content {
  padding: 1rem 0;
}
</style>