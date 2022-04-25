<template>
  <article>
        <img :src="require('@/assets/images/' + product.image)" alt="" class="product__preview">
        <span class="product__price">{{ product.price }} ₽</span>
        <h4 class="product__name">{{ product.name.slice(0, 30) + '...' }}</h4>
        <div class="product__footer">
            <v-switcher />
            <button @click="$emit('add', product)" class="product__cart-btn" >В корзину</button>
        </div>
    </article>
</template>

<script>
import vSwitcher from '@/components/v-switcher.vue'

export default {
    props: {
        product: Object
    },

    components: {
        vSwitcher
    }
}
</script>



<style>
/* .product {
    margin: 10px;
    width: calc(25% - 20px);
    background-color:#e8e8e4;
    padding: 30px 20px;
    border-radius: 20px;
} */
.product__preview {
    width: 100%;
    height: 350px;
}
.product__price {
    font-size: 18px;
    
    line-height: 24px;
    color: #000;
    font-weight: 700;
    margin-right: 10px;
}


.product__cart-btn {
    width: 100%;
    height: 30px;

    font-size: 20px;
    background: #81b29a;
    border: none;
    margin-top: 10px;
    border-radius: 26px;
}
</style>