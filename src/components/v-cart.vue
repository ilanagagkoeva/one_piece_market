<template>
  <div class="cart">
        <button class="cart__btn" @click="cartVisible = !cartVisible">
            <i class="cart__btn-icon">
                <div class="cart__amount">1</div>
            </i>
            <!-- <span class="cart__btn-label">Корзина</span> -->
        </button>

        <div class="cart__list" v-if="cartVisible">
            <div class="cart-item" v-for="p in basket" :key="p.vendorCode">
                <img :src="require('@/assets/images/' + p.image)" alt="" class="cart-item__preview">
                <span class="cart-item__name">{{ p.name }}</span>
                <v-switcher />
                <span class="cart-item__price">{{ p.price }} ₽</span>
                <a href="#" class="cart-item__remove" @click.prevent="$emit('remove', p.vendorCode)">Удалить</a>
            </div>
            
            <slot />

        </div>

    </div>
</template>

<script>
import vSwitcher from '@/components/v-switcher.vue'

export default {
    components: {
        vSwitcher
    },
    props: {
        basket: Array,
    },
    data() {
        return {
            cartVisible: false
        }
    }
}
</script>

<style>
.cart {
    position: relative;
    
}

.cart__btn {
    width: 30px;
    height: 29px;
    display: flex;
    flex-direction: column;
    align-items: center;
    border: none;
    background-color: transparent;
    cursor: pointer;
    
}

.cart__amount {
    font-size: 10px;
    line-height: 13px;
    text-transform: uppercase;
    color: #fff;
    text-align: center;
    display: inline-block;
    min-width: 16px;
    height: 16px;
    position: absolute;
    top: -6px;
    right: -8px;
    background: #f55123;
    padding: 2px 3px 1px;
    border-radius: 16px;
}

.cart__btn:hover .cart__btn-label {
    color: #fff;
}

.cart__btn-icon {
    margin-bottom: 6px;
    width: 27px;
    height: 27px;
    background: url(data:image/svg+xml,%3Csvg%20width%3D%2227%22%20height%3D%2224%22%20viewBox%3D%220%200%2027%2024%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Cpath%20fill-rule%3D%22evenodd%22%20clip-rule%3D%22evenodd%22%20d%3D%22M8.5%201.5C8.5%202.5%206%202.5%204.5%202.5C3%202.5%200.5%202.5%200.5%201.5C0.5%200.5%203%200.5%204.5%200.5C6%200.5%208.5%200.5%208.5%201.5ZM11.8212%2016.119C11.3452%2016.1949%2010.8829%2015.9206%2010.7214%2015.4665L7.48289%206.35812C7.24913%205.70067%207.74355%205.01199%208.44122%205.02324L25.8008%205.30317C26.425%205.31324%2026.8875%205.88644%2026.7654%206.49865L25.4106%2013.2909C25.3288%2013.701%2025.0004%2014.017%2024.5874%2014.0828L11.8212%2016.119ZM13.6523%2021.0331C13.6523%2022.3178%2012.6109%2023.3593%2011.3262%2023.3593C10.0415%2023.3593%209%2022.3178%209%2021.0331C9%2019.7484%2010.0415%2018.707%2011.3262%2018.707C12.6109%2018.707%2013.6523%2019.7484%2013.6523%2021.0331ZM22.957%2023.3593C24.2417%2023.3593%2025.2832%2022.3178%2025.2832%2021.0331C25.2832%2019.7484%2024.2417%2018.707%2022.957%2018.707C21.6723%2018.707%2020.6309%2019.7484%2020.6309%2021.0331C20.6309%2022.3178%2021.6723%2023.3593%2022.957%2023.3593Z%22%20fill%3D%22white%22%2F%3E%0A%3C%2Fsvg%3E%0A) center/contain no-repeat;
    position: relative;
    font-style: normal;
}

.cart__btn-label {
    font-size: 14px;
    line-height: 20px;
    color: rgba(255,255,255,.6);
    text-decoration: none;
    display: block;
    transition: color .3s ease 0s;
}

.cart__list {
    border-radius: 10px;
    padding: 40px 20px;
    position: absolute;
    right: 0;
    top: 100%;
    z-index: 3;
    width: 600px;
    
    background-color: #edf2fb;
    
    
}

.cart-item {
    padding: 15px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.cart-item__name {
    font-size: 14px;
    line-height: 20px;
    color: #999;
    font-weight: 400;
}

.cart-item__preview {
    width: 48px;
    height: 58px;
    object-fit: cover;
}

.cart-item__price {
    font-size: 14px;
    line-height: 20px;
    font-weight: 700;
}

.cart-item__remove {
    font-size: 14px;
    line-height: 20px;
    color: #999;
    font-weight: 700;
    text-decoration: none;
}
.switcher__value{
    width: 60%;
}
.cart-item__remove:hover {
    color: #000;
}
</style>