<template>
    <header>
        <!-- <div class="container">
            <div class="header">
                <img src="@/assets/images/logo.png" alt="logo" class="header__logo">
                
                
                <v-cart :basket="cart" @remove="removeFromCart">
          <h1>lorem</h1>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet rerum cumque et velit non temporibus quidem consequuntur suscipit. Amet ex laudantium illum, aliquid modi neque laboriosam asperiores ad incidunt autem.</p>
        </v-cart>
        
            </div>
        </div> -->

        <div class="container">
      <div class="header">
        
          <img src="@/assets/images/logo.png" alt="logo" class="header__logo">
        
          <div class="container-for-search">
          <input type="text" class="header__search-input" placeholder="Найти..." v-model="search">
          <div class="container-for-res">
           
          <div class="result-of-search" v-for="product in filteredList" v-bind:key="product">
            {{product.name}}
            
          </div>
          
          </div>
          </div>
          <button class="header__search-button"></button>
        

        <v-cart :basket="cart" @remove="removeFromCart">
          <h1>lorem</h1>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet rerum cumque et velit non temporibus quidem consequuntur suscipit. Amet ex laudantium illum, aliquid modi neque laboriosam asperiores ad incidunt autem.</p>
        </v-cart>
        

      </div>
    </div>
    </header>
    
      <div class="container">
        <carousel :items-to-show="1" :wrapAround="true" :pauseAutoplayOnHover="true">
          
          <slide v-for="p in products" :key="p.vendorCode" class="container-slider">
            <img :src="require('@/assets/images/' + p.image)" alt="" class="slider-image">
          </slide>
          
          <template #addons>
            <navigation />
            <pagination />
          </template>
          
        </carousel>
      </div>
    <main>
        
        <div class="container">
            <section class="products">
            <div class="products__head">
                <span class="products__amount">3 899 товаров</span>
            <div class="products__view">
            <button class="product__view-btn product__view-btn--large " v-bind:class="isActive===true? 'product__view-btn--active': none" @click="isActive = !isActive" ></button>
            <button class="product__view-btn product__view-btn--small" v-bind:class="isActive===false? 'product__view-btn--active': none" @click="isActive = !isActive"></button>
          </div>
            </div>
            <div class="products__list">
                <v-product 
                  v-bind:class="isActive? 'active-class': 'product-three' "
                  v-for="product in paginatedData"
                  :key="product.vendorCode"
                  :product="product"
                  @add="addToCart"
                />
        </div>
         <div class="pagination">
           <button @click="previousPage" :disabled="pageNumber===0" class="previous">Предыдущая</button>
              <ul class="pagination__list">
                <li class="pagination__item " v-bind:class="pageNumber===0? 'pagination__item--active': none"> 1</li>
                <li class="pagination__item" v-bind:class="pageNumber===1? 'pagination__item--active': none">2</li>
                
              </ul>
          <button @click="nextPage" :disabled="pageNumber >= pageCount-1" class="next">Следующая</button>
        </div>
            </section>
        </div>
    </main>
     <footer>
    <div class="container">
            <div class="footer">
              <p class="footer__copyright">
                1997-2021 &copy; One piece <br> автор Эйитиро Ода.
              </p>
            </div>
          </div>
  </footer>
</template>
<script>
import vProduct from '@/components/v-product.vue'
import vCart from '@/components/v-cart.vue'
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
export default{
  components: {
      vCart,
      vProduct,
      Carousel,
      Slide,
      Pagination,
      Navigation,

  },
  data() {
    return {
      products: [
        { name: 'One Piece Том 1', image: 'onepiece1.jpg', price: 1030, vendorCode: 'A1' },
        { name: 'One Piece Том 2', image: 'onepiece2.webp', price: 1200, vendorCode: 'A2' },
        { name: 'One Piece Том 3', image: 'onepiece3.jpg', price: 1111, vendorCode: 'A3' },
        { name: 'One Piece Том 4', image: 'onepiece4.jpg', price: 1234, vendorCode: 'A4' },
        { name: 'One Piece Том 5', image: 'onepiece5.jpg', price: 1400, vendorCode: 'A5' },
        { name: 'One Piece Том 6', image: 'onepiece6.webp', price: 1560, vendorCode: 'A6' },
        { name: 'One Piece Том 7', image: 'onepiece7.webp', price: 1860, vendorCode: 'A7' },
        { name: 'One Piece Том 8', image: 'onepiece8.webp', price: 1160, vendorCode: 'A8' },
        { name: 'One Piece Том 9', image: 'onepiece9.webp', price: 1260, vendorCode: 'A9' },
        { name: 'One Piece Том 10', image: 'onepiece10.jpg', price: 1230, vendorCode: 'A10' },
        { name: 'One Piece Том 11', image: 'onepiece11.webp', price: 1320, vendorCode: 'A11' },
        { name: 'One Piece Том 12', image: 'onepiece12.webp', price: 1030, vendorCode: 'A12' },
      ],

      cart: [],
      search: '',
      isActive: true,
      currentPage: 1,
       pageNumber: 0,
       isPage: true,
       

    }
  },

  methods: {
    addToCart(product) {
      this.cart.push(product)

      this.$swal('Товар добавлен в корзину')
    },

    removeFromCart(vendorCode) {
      this.cart = this.cart.filter(e => e.vendorCode !== vendorCode)
    },
    nextPage(){
            this.pageNumber++;
        },
    previousPage(){
        this.pageNumber--;
    }
  },
  
  computed: {
    filteredList() {
      if (this.search !== ''){
      const result= this.products.filter(product => {
        return product.name.toLowerCase().includes(this.search.toLowerCase())
      })
      console.log(result, this.search)
      return result
      }
      else {
        return []
      }
    },
    pageCount() {
            let len = this.products.length;
            let size = this.sizeOfList;
            return Math.ceil(len/size);
            
        },
    paginatedData(){
        const start = this.pageNumber * this.sizeOfList;
        const end = start + this.sizeOfList;
        return this.products.slice(start, end);

    }
  },
  props: {
        sizeOfList: {
            type: Number,
            required: false,
            default: 6
        }
    },



}
   
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200&display=swap');
*, *::before, *::after{
    box-sizing: border-box;
    font-family: Montserrat;
}
body {
    margin: 0;
    padding: 0;
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;

    /* background: url('@/assets/images/luffy.jpg'); */
    background-image: url("assets/images/luffy.jpg");
    /* b
    background-image: url('assets/images/background_anime_onepiece.jpg');
    background-size: 150%;
    background-position-x: -650px; */
}
.container-slider {
  width: 100%;
  height: 350px;
  position: relative;
  /* background: white; */
  padding: auto 0;;
}
.slider-image {
  width: calc(25% - 20px);
  height: 100%;
   top: 0;
  left: 0;
  position: absolute;
  display: block;
    margin-left: 40%;
    margin-right: 40%;
}
.product__view-btn {
    margin: 0 5px;
    width: 18px;
    height: 18px;
    border: none;
    background-color: transparent;
    cursor: pointer;
}

.product__view-btn--large {
    background-image: url(data:image/svg+xml,%3Csvg%20width%3D%2241%22%20height%3D%2218%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Crect%20x%3D%2222%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2228.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2235.203%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2235.203%22%20y%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2228.6%22%20y%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2222%22%20y%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2222%22%20y%3D%2213.199%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2228.6%22%20y%3D%2213.199%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2235.203%22%20y%3D%2213.199%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%2213.203%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%2213.203%22%20y%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%226.6%22%20y%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20y%3D%226.6%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20y%3D%2213.199%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%226.6%22%20y%3D%2213.199%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%2213.203%22%20y%3D%2213.199%22%20width%3D%224.8%22%20height%3D%224.8%22%20rx%3D%222.4%22%20fill%3D%22%23E8E8E8%22%2F%3E%3C%2Fsvg%3E);
    background-position: 0 0;
}

.product__view-btn--small {
    background-image: url(data:image/svg+xml,%3Csvg%20width%3D%2245%22%20height%3D%2218%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Crect%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%2210.203%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%2210.203%22%20y%3D%2210.199%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20y%3D%2210.199%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23E8E8E8%22%2F%3E%3Crect%20x%3D%2226%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2236.203%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2236.203%22%20y%3D%2210.199%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23CB11AB%22%2F%3E%3Crect%20x%3D%2226%22%20y%3D%2210.199%22%20width%3D%227.8%22%20height%3D%227.8%22%20rx%3D%223.9%22%20fill%3D%22%23CB11AB%22%2F%3E%3C%2Fsvg%3E);
    background-position: 0 0;
}

.product__view-btn--active {
    background-position-x: 19px ;
}

.container {
    width: 100%;
    max-width: 1300px;
    padding: 0 15px;
    margin: 0 auto;
}
header{
   border-radius: 24px;
    /* background: linear-gradient(to left, #ced4da 0, #d8e2dc 100%) no-repeat ; */
    /* opacity: 0.1; */

}
.header {
    padding: 30px 0 50px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.header__logo {
    margin-top: 6px;
    margin-right: 16px;
    width: 360px;
    height: 100px;

}


.header__search-button {
    top: 50%; 
   
    width: 24px;
    height: 24px;
    margin-left: 15px;
    background-image: url(data:image/svg+xml,%3Csvg%20width%3D%2248%22%20height%3D%2224%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%3Cpath%20d%3D%22M38.7%2013.5l-.2.3a6%206%200%2010-.6.6l-.6.4%204.7%204.5a1%201%200%20001.3-1.3l-4.6-4.5zM34%2014a4.1%204.1%200%20110-8.3%204.1%204.1%200%20010%208.3z%22%20fill%3D%22%23B6B6B6%22%2F%3E%3Cpath%20d%3D%22M14.7%2013.5l-.2.3a6%206%200%2010-.6.6l-.6.4%204.7%204.5a1%201%200%20001.3-1.3l-4.6-4.5zM10%2014a4.1%204.1%200%20110-8.3%204.1%204.1%200%20010%208.3z%22%20fill%3D%22%23fff%22%2F%3E%3C%2Fsvg%3E);
    background-color: transparent;
    border: none;
}
main {
    
    position: relative;
    z-index: 2;
    /* background-color: rgb(248, 248, 248); */
    margin-top: 3px;
    padding: 60px 0;
    /* border-radius: 26px; */
    /* background: #e8e8e4; */
}

.products__head {
    margin-bottom: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.products__amount {
    margin-left: auto;
    margin-right: auto;
    font-weight: bold;
    font-size: 14px;
    line-height: 20px;
    color: #8b8b8b;

}


.products__list {

    display: flex;
    flex-wrap: wrap;
    
}
.active-class {
    margin: 10px;
    width: calc(25% - 20px);
    background-color:#e8e8e4;
    padding: 30px 20px;
    border-radius: 20px;
}
.product-three {
    margin: 10px;
    width: calc(30% - 20px);
    background-color:#e8e8e4;
    padding: 30px 20px;
    border-radius: 20px;
}
.carousel__prev, .carousel__next {
    background-color: #81b29a;
}
.carousel__pagination-button {
    background-color: #81b29a;
}

.carousel__pagination-button--active {
    background-color: blue;
}
/* SEARCHHHHHHHHHHHHHH */
.container-for-search {
    position: relative;
    /* display: flex; */
    width: 100%;
    /* flex-wrap: wrap; */
    /* padding-top: 12px; */
}
.container-for-res {
  /* margin-top: 60px; */
  /*  
      padding-left: 12px; */
     
      margin-left: 5px;
  position: absolute;
  width:100%;
  z-index: 2;
}
.result-of-search {  

        padding-bottom: 15px;
      background: white;
      text-decoration: none;  
      color: black;
      font-size: 24px;
      z-index: 2;
      
}

.header__search-input {
  position: relative;
    outline: none;
    border: none;
    font-size: 18px;
    line-height: 24px;
    transition: background .3s ease 0s;
    color: black;
    width:100%;
    padding: 16px 120px 16px 50px;
    
    margin-left: 5px;
    margin-right: 5px;
    background: white;
    cursor: pointer;
    appearance: none;
}
.pagination {
    padding: 30px 0;
    display: flex;
    justify-content: center;
   
}

.pagination__list {
    display: flex;
    list-style: none;
    padding: 0;
    margin: 0;
}

.pagination__item {
    width: 37px;
    height: 37px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: white;
    color: black;
}

.pagination__item:not(.pagination__item--active):hover {
    background-color: #f2f2f2;
    cursor: pointer;
}

.pagination__item--active {
    background-color: #81b29a;
    color: white;
}
.previous {
  background-color: #81b29a;
    color: white;
}
.next {
  background-color: #81b29a;
    color: white;
}

footer {
    margin-top: auto;
    background-color: white;
}

.footer {
    padding: 30px 0;
}

.footer__copyright {
    text-align: center;
    font-size: 14px;
    line-height: 20px;
    color: #81b29a;
}

</style>