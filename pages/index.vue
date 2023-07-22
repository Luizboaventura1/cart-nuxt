<template>
  <v-app theme="dark">
    <v-container class="mx-auto">
      <div
        class="title-box py-5 px-4 w-100"
      >
        <h1
          class="font-weight-bold"
        >
          Products
        </h1>
      </div>
      <div
        class="container-products w-100"
      >
        <v-row>
          <v-col
            v-for="(product,index) in listProducts"
            :key="index"
            cols="12"
            sm="3"
            class="pa-3 d-flex justify-center"
          >
            <v-card
              class="bg-grey-darken-4 elevation-5 rounded pa-3"
            >
              <v-card-title
                class="font-weight-bold px-0"
              >
                {{ product.product }}
              </v-card-title>
              <v-card-title
                class="text-white px-0"
              >
                R$ {{ product.price.toFixed(2).replace('.',',') }}
              </v-card-title>
              <v-card-subtitle
                class="mb-4 px-0"
              >
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quae, quis!
              </v-card-subtitle>
              <v-btn
                @click="addCart(index)"
                class="bg-blue-lighten-1 w-100 font-weight-bold"
              >
                Add cart
              </v-btn>
            </v-card>
          </v-col>
        </v-row>
      </div>
      <div class="cart py-7">
        <div class="px-4">
          <h1 class="font-weight-bold">Cart</h1>
        </div>
        <div
          class="container-cart"
        >
        <v-row>
          <v-col
            v-for="(product,index) in cart"
            :key="index"
            cols="12"
            sm="3"
            class="pa-3"
          >
            <v-card
              class="bg-grey-darken-4 elevation-5 rounded pa-3"
            >
              <v-card-title
                class="font-weight-bold px-0"
              >
                {{ product.product }}
              </v-card-title>
              <v-card-title
                class="text-white px-0"
              >
                R$ {{ product.price.toFixed(2).replace('.',',') }}
              </v-card-title>
              <v-card-subtitle
                class="mb-4 px-0"
              >
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quae, quis!
              </v-card-subtitle>
              <div class="quantity-buttons w-100 d-flex py-2">
                <BtnMore 
                  @click="btnMore(index)"
                />
                <div
                  class="quantity-products-cart bg-white text-black d-flex justify-center align-center"
                >
                  {{ product.quantity }}
                </div>
                <BtnMinus 
                  @click="btnMinus(index)"
                />
                <v-btn
                  @click="deleteItemCart(index)"
                  class="bg-red-accent-4 text-white font-weight-bold ms-5 px-2"
                >
                  Delete
                </v-btn>
              </div>
              <v-btn
                class="bg-blue-lighten-1 w-100 font-weight-bold"
              >
                Buy
              </v-btn>
            </v-card>
          </v-col>
        </v-row>
      </div>
      </div>
    </v-container>
  </v-app>
</template>

<script setup>
import { ref } from 'vue';
import BtnMinus from '@/components/Buttons/BtnMinus.vue'
import BtnMore from '@/components/Buttons/BtnMore.vue'

let listProducts = ref([
  {product: 'Agua',price: 100,quantity:1},
  {product: 'Calça',price: 200,quantity:1},
  {product: 'FIFA',price: 60,quantity:1},
  {product: 'Biscoito',price: 10,quantity:1}
])

let cart = ref([])

const addCart = (index) => {
  if(cart.value[index] == listProducts.value[index]) {
    cart.value[index].quantity += 1
  }else {
    cart.value.push(listProducts.value[index])
  }
}

const btnMore = (index) => {
  cart.value[index].quantity += 1
}

const btnMinus = (index) => {
  (cart.value.at(index).quantity > 0) ? cart.value.at(index).quantity -= 1 : cart.value.at(index).quantity
}

const deleteItemCart = (index) => {
  cart.value.splice(index, 1)
}

useHead({
  title: 'My Cart',
  meta: [
    { name: 'description', content: 'My amazing site.' },
    { name: 'author', content: 'Luiz'}
  ],
  script: [ { innerHTML: 'console.log(\'Hello world\')' } ]
})

</script>

<style scoped lang="scss">

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.quantity-buttons {
  .quantity-products-cart {
    width: 50px;
    height: 30px;
    border: 2px solid black;
  }
}
</style>