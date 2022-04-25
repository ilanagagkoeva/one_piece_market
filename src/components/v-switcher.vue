<template>
  <div class="switcher product__switcher">
        <button @click="val--" class="switcher__btn switcher__btn--plus">-</button>
        <input class="switcher__value" :value="val">
        <button @click="val++" class="switcher__btn switcher__btn--minus">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            val: 1
        }
    },

    watch: {
        val(newVal) {
            if (newVal < 1) {
                this.val = 1
            }
        }
    }
}
</script>

<style>
.switcher {
    display: flex;
    
}
.switcher__btn--plus {
    background: #d8e2dc;
    border: none;
    width: 30px;
    height: 30px;
    border-radius: 26%;
    
}
.switcher__btn--minus {
    background: #d8e2dc;
    border: none;
    width: 30px;
    height: 30px;
    border-radius: 26%;
}
.switcher__value {
    background: white;
    border: none;
    
    min-width: 80%;
    height: 30px;
    border-radius: 26px;
    font-weight: bold;
    margin-left: 1px;
    margin-right: 1px;
    text-align: center;
}

</style>