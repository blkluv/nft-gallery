<template>
  <b-field class="file is-primary" :class="{ 'has-name': !!file }">
    <b-upload v-model="file" class="file-label" expanded>
      <span class="file-cta">
        <img
          src="@/assets/camera_dark.png"
          alt="First NFT market explorer on Kusama and Polkadot"
          class="ico-media"
        />
        <span class="file-label" style="margin-left:35px;letter-spacing:1.1px">{{ label }}</span>
      </span>
      <span class="file-name" v-if="file">
        {{ file.name }}
      </span>
    </b-upload>
    <Tooltip iconsize="is-medium" label="Upload your image of the NFT" />
  </b-field>
</template>

<script lang="ts" >
import { Component, Prop, Vue, Watch, Emit } from "vue-property-decorator";
import Tooltip from "@/components/shared/Tooltip.vue";

@Component({
  components: {
    Tooltip,
  },
})
export default class extends Vue {
  @Prop({ default: "Choose File" }) public label!: string;
  @Prop({ default: "file-image" }) public icon!: string;
  private file: Blob | null = null;

  @Watch("file")
  public createInput(file: Blob): void {
    const reader = new FileReader();
    reader.onload = () => {
      // this.handleSelection(reader.result)
      // console.log(reader.result);
    };
    this.$emit("input", file);
    reader.readAsText(file);
  }

  @Emit("change")
  public handleSelection(value: string | ArrayBuffer | null) {
    return value;
  }
}
</script>
<style scoped>
.ico-media {
  width: 20px;
  height: 20px;
  position: absolute;
  left: 10px;
}

</style>