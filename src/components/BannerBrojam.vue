<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel class="product-slider" :items="3" :nav="false" :autoplay="true" :dots="false">
                        
                        <div class="product-item" v-for="item in products" v-bind:key="item.id">
                            <div class="pi-pic">
                                <img v-bind:src="item.galleries[0].photo" alt="" />
                                <ul>
                                    <li @click="saveKeranjang(item.id, item.name, item.price, item.galleries[0].photo)" class="w-icon active">
                                        <a href="#">
                                            <i class="icon_bag_alt"></i>
                                        </a>
                                    </li>
                                    <li class="quick-view">
                                        <router-link v-bind:to="'/product/'+item.id">+ Quick View</router-link>
                                    </li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{item.type}}</div>
                                <router-link to="/product">
                                    <h5>{{item.name}}</h5>
                                </router-link>
                                <div class="product-price">
                                    ${{item.price}}
                                    <span>${{item.price}}</span>
                                </div>
                            </div>
                        </div>

                    </carousel>
                </div>
                <div v-else class="col-lg-12 mt-5">
                    <h3>Produk terbaru belum tersedia untuk saat ini.</h3>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->    
</template>

<script>
import carousel from 'vue-owl-carousel'
import axios from 'axios'

export default {
    name: 'BannerBrojam',
    components: {
        carousel
    },
    data() {
        return {
            products: [],
            keranjangUser: []
        };
    },
    methods: {
        saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct) {
            var productStored = {
                "id": idProduct,
                "name": nameProduct,
                "price": priceProduct,
                "photo": photoProduct
            }

            this.keranjangUser.push(productStored);
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
            window.location.reload();
        }
    },
    mounted() {
        axios
        .get("http://127.0.0.1:8000/api/products")
        .then(res => (this.products = res.data.data.data))
        // eslint-disable-next-line no-console
        .catch(err => console.log(err));
        if(localStorage.getItem('keranjangUser')) {
            try {
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch(e) {
                localStorage.removeItem('keranjangUser');
            }
        }
    }
}
</script>

<style scoped>
.product-item {
    margin-right: 25px;
}

.pi-pic {
    max-height: 500px;
}
</style>