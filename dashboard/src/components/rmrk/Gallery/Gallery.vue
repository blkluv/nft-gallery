<template>
  <div>
    <div>
      <div class="columns is-multiline">
        <div class="column is-4" v-for="nft in nfts" :key="nft.id">
          <div class="card nft-card">
            <router-link
              :to="{ name: 'nftDetail', params: { id: nft.id } }"
              tag="div"
              class="nft-card__skeleton"
            >
              <div class="card-image" v-if="nft.image">
                <b-skeleton height="240px" :active="isLoading"> </b-skeleton>
                <b-image
                  v-if="!isLoading"
                  :src="nft.image"
                  :src-fallback="require('@/utils/placeholder.png')"
                  alt="Simple image"
                  ratio="1by1"
                ></b-image>
              </div>

              <div v-else class="card-image">
                <b-image
                  :src="
                    require('@/assets/kodadot_logo_v1_transparent_400px.png')
                  "
                  alt="Simple image"
                  ratio="1by1"
                ></b-image>
              </div>

              <div class="card-content">
                <div class="collectible-card__price-item-container">
                  <div class="collectible-card__price-item">
                    <a
                      class="collectible-card__price-number"
                      href="/artwork-v2/eight-phoenix-16158"
                      ><div
                        style="
                          overflow: hidden;
                          text-overflow: ellipsis;
                          white-space: nowrap;
                        "
                      >
                        <span>0.258</span
                        ><span class="eth-symbol" style="font-size: 15px"
                          >Ξ</span
                        >
                        ($<span>450</span>)
                      </div></a
                    >
                    <p class="collectible-card__price-text">List price</p>
                  </div>
                  <div class="collectible-card__price-item">
                    <a
                      class="collectible-card__price-number"
                      href="/artwork-v2/eight-phoenix-16158"
                      ><span>0.11</span
                      ><span class="eth-symbol" style="font-size: 15px">Ξ</span>
                      ($<span>198</span>)</a
                    >
                    <p class="collectible-card__price-text">
                      Current offer by<a
                        class="collectible-card__price-username"
                        href="/erosandagape"
                        >@erosandagape</a
                      >
                    </p>
                  </div>
                </div>
                <hr />
                <p v-if="!isLoading" class="title is-4 has-text-centered">
                  <router-link
                    :to="{ name: 'nftDetail', params: { id: nft.id } }"
                  >
                    {{ nft.name }}
                  </router-link>
                </p>
                <b-skeleton :active="isLoading"> </b-skeleton>
              </div>
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" >
import { Component, Prop, Vue, Watch } from "vue-property-decorator";
import { getInstance } from "@/components/rmrk/service/RmrkService";
import { NFTWithMeta, NFT } from "../service/scheme";
import { defaultSortBy, sanitizeObjectArray } from "../utils";
import GalleryCardList from "./GalleryCardList.vue";

type NFTType = NFT | NFTWithMeta;
const components = { GalleryCardList };

@Component({ components })
export default class Gallery extends Vue {
  private nfts: NFTType[] = [];
  private isLoading: boolean = true;

  public async mounted() {
    const rmrkService = getInstance();

    if (!rmrkService) {
      return;
    }

    try {
      this.nfts = await rmrkService
        .getAllNFTs()
        .then(sanitizeObjectArray)
        .then(defaultSortBy);
      // this.collectionMeta();
    } catch (e) {
      console.warn(e);
    }

    this.isLoading = false;
  }
}
</script>

