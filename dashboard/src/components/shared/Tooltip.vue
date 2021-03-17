<template>
  <p class="control">
    <b-tooltip
      type="is-primary is-light"
      size="is-small"
      position="is-left"
      :label="label"
      multilined
      square
    >
      <img
        src="@/assets/message.png"
        alt="First NFT market explorer on Kusama and Polkadot"
        class="ico-message"
      />
    </b-tooltip>
  </p>
</template>

<script lang="ts" >
import { Component, Prop, Vue, Watch } from "vue-property-decorator";

@Component({})
export default class Tooltip extends Vue {
  @Prop() public label!: string;
  @Prop({ default: "is-large" }) public iconsize!: string;
}
</script>
<style scoped>
.ico-message {
  width: 40px;
  height: 40px;
}
</style>
