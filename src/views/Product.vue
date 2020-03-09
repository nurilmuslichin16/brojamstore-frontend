<template>
  <div class="Product">
    <HeaderBrojam />

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
                        <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="gambarUtama" alt="" />
                            </div>
                            <div class="product-thumbs">
                                <carousel :dots="false" :nav="false" class="product-thumbs-track ps-slider" v-if="productDetail.galleries.length > 0">
                                    <div v-for="g in productDetail.galleries" :key="g.id" @click="(changeImage(g.photo))" :class="g.photo == gambarUtama ? 'active' : '' " class="pt">
                                        <img :src="g.photo" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6 text-left">
                            <div class="product-details">
                                <div class="pd-title">
                                    <span>{{ productDetail.type }}</span>
                                    <h3>{{ productDetail.name }}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p v-html="productDetail.description"></p>
                                    <h4>${{ productDetail.price }}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart" class="primary-btn pd-cart">Add To Cart</router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedBrojam />
    <FooterBrojam />
  </div>
</template>

<script>
import HeaderBrojam from '@/components/HeaderBrojam.vue'
import FooterBrojam from '@/components/FooterBrojam.vue'
import RelatedBrojam from '@/components/RelatedBrojam.vue'
import carousel from 'vue-owl-carousel'

import axios from 'axios'

export default {
  name: 'Product',
  components: {
    HeaderBrojam,
    FooterBrojam,
    RelatedBrojam,
    carousel
  },
  data() {
      return {
          gambarUtama: '',
          productDetail: []
      }
  },
  methods: {
      changeImage(imgURL){
          this.gambarUtama = imgURL;
      },
      setDataPicture(data){
          // replace object productDetail dengan data dari API
          this.productDetail = data;
          // replace value gambar default dengan data dari API (galleries)
          this.gambarUtama = data.galleries[0].photo;
      }
  },
    mounted() {
        axios
        .get("http://127.0.0.1:8000/api/products", {
            params: {
                id: this.$route.params.id
            }
        })
        .then(res => (this.setDataPicture(res.data.data)))
        // eslint-disable-next-line no-console
        .catch(err => console.log(err));
    }
}
</script>

<style scoped>
.product-thumbs .pt {
    margin-right: 10px;
}
</style>