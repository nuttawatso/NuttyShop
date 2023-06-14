<template>
    <div class="d-flex justify-content-center" v-if="!product_store.load_products">
        <h2>Loading...</h2>

    </div>
    
   <div class="row mt-2">
    <div class="col mb-3" v-for="(product ,index) in search_products" key="index">
        <div class="card h-100" >
            <img :src="product.image" alt="" class="card-img-top mx-auto">
            <div class="card-body p-4">
                <h5 class="card-title">{{ product.title }}</h5>
                <p class="card-text">หมวดหมู่ {{ product.category }}</p>
                <p class="card-text">ราคา {{ currencyTHB(product.price) }} บาท</p>
                <div>
                    <routerLink :to="`/product_detail/${product.id}`" class="btn btn-dark mx-2">รายละเอียด</routerLink>
                    <button class="btn btn-dark " @click="cart_store.add_cart(product.id,product.price)">เพิ่มลงตะกร้า</button>
                </div>

            </div>
        </div>
    </div>
   </div>

  </template>
  
<script setup>
import { computed } from 'vue';

//currencyTHB
import { currencyTHB } from '../shared/currency';
//useProductStore
import { useProductStore } from '../store/product';
const product_store = useProductStore()

const list = computed(() => product_store.list_products)

const search_products = computed(() => product_store.search_products)

//usecartstore

import { useCartStore } from '../store/cart';
 const cart_store = useCartStore()


</script>


<style scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.card{
    width: 19rem;

    border-radius: 1rem;
}
.card .card-body{
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
    
}
/* .card:hover{
    background-color: rgb(62, 62, 62);
    color: white;
    transform: scale(1.03);
    transition: all 1s ease;

} */
.card img{
    margin-top: 1rem;
    width: 12rem;
    height: 12rem;
    
   
}
.card-body {
   text-align: center;
}
.card-body .btn {
   margin-top: 1rem;
}

@media screen and (max-width: 412px) {
    .card{
        margin: auto;
    }
    
}

@media screen and (max-width: 820px) {
    .card{
        margin: auto;
    }
    
}

@media screen and (max-width: 1024px) {
    .card{
        margin: auto;
 
    }
    
}
</style>
