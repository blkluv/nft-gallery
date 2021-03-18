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
                <p v-if="!isLoading" class="title is-4">
                  <router-link
                    :to="{ name: 'nftDetail', params: { id: nft.id } }"
                  >
                    {{ nft.name }}
                  </router-link>
                </p>
                <div class="collectible-card__price-item-container">
                  <div>
                    <p class="collectible-card__price-text">
                      List price:&nbsp;&nbsp;&nbsp;0.258<span class="eth-symbol" style="font-size: 15px"
                          >Ξ</span
                        >
                        ($<span>450</span>)
                    </p>
                  </div>
                  <div>
                    <p class="collectible-card__price-text">
                      Current offer:&nbsp;&nbsp;&nbsp;0.11<span class="eth-symbol" style="font-size: 15px"
                          >Ξ</span
                        >
                        ($<span>198</span>)</a>
                    </p>
                  </div>
                </div>

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
<style lang="scss" scoped>
.card.nft-card {
  background-color: white;
  a,
  p,
  span,
  div {
    color: black;
    font-family: "Archivo", sans-serif !important;
  }
  p {
    margin-bottom: unset;
  }
}
</style>
