<template>
  <div class="card nft-card">
    <LinkResolver class="nft-card__skeleton" :route="type" :param="id" :link="link" tag="div" >
      <div class="card-image" v-if="image">
        <b-image
          :src="image"
          :src-fallback="require('@/assets/kodadot_logo_v1_transparent_400px.png')"
          alt="Simple image"
          ratio="1by1"
        ></b-image>
      </div>

      <div v-else class="card-image">
        <b-image
          :src="require('@/assets/kodadot_logo_v1_transparent_400px.png')"
          alt="Simple image"
          ratio="1by1"
        ></b-image>
      </div>

      <div class="card-content">
        <p class="title is-4 has-text-centered has-text-primary">
          {{ name }}
        </p>
      </div>
    
    </LinkResolver>
  </div>
</template>

<script lang="ts" >
import { Component, Prop, Vue } from 'vue-property-decorator';

const components = {
  LinkResolver: () => import('@/components/shared/LinkResolver.vue')
}

@Component({ components })
export default class GalleryCard extends Vue {
  @Prop({ default: 'nftDetail' }) public type!: string;
  @Prop({ default: 'rmrk/detail' }) public link!: string;
  @Prop() public id!: string;
  @Prop() public name!: string;
  @Prop() public image!: string;
}
</script>

<style>
.card.nft-card {
  padding: 1em !important;
  height: 100%;
  border: solid 1px gray;
}
.card-content{
  height: 100%;
  padding:1.5rem 0;
}
.nft-card__skeleton {
  display: flex;
  height: 100%;
  flex-direction: column;
  justify-content: space-between;
  cursor: pointer;
}
.collectible-card__price-item-container {
    display: block;
    padding-top: 8px;
}
.collectible-card__price-item {
    width: 100%;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}
.collectible-card__price-number {
    font-family: "Founders Grotesk Regular";
    font-size: 18px;
    margin-bottom: 0;
    word-wrap: break-word;
    color: #2d8e69;
}
.collectible-card__price-text {
    font-family: "Founders Grotesk Regular";
    display: -ms-flexbox;
    display: flex;
    font-size: 12px;
    margin-bottom: 0;
    white-space: nowrap;
    color: #005c3a;
}
.collectible-card__price-username {
    display: inline-block;
    padding-left: 2px;
    color: #005c3a;
    overflow: hidden;
    white-space: nowrap;
    max-width: 85px;
}
a {
    text-decoration: none;
}
hr {
    margin-top: 20px;
    margin-bottom: 20px;
    border: 0;
    border-top: 1px solid #eee;
}
a {
  color: grey;
}
.collectible-card__price-text {
  color: rebeccapurple;
}
</style>
