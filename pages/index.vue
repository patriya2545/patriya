<template>
  <div>
    <div>
      <div
        class="px-4 py-16 mx-auto sm:max-w-xl md:max-w-full lg:max-w-screen-xl md:px-24 lg:px-8 lg:py-20"
      >
        <div class="max-w-xl sm:mx-auto lg:max-w-2xl">
          <div class="flex flex-col mb-16 sm:text-center sm:mb-0">
            <div
              class="max-w-xl mb-10 md:mx-auto sm:text-center lg:max-w-2xl md:mb-12"
            >
              <h2
                class="max-w-lg mb-6 font-sans text-3xl font-bold leading-none tracking-tight text-gray-900 sm:text-4xl md:mx-auto"
              >
                <span class="relative inline-block">
                  <svg
                    viewBox="0 0 52 24"
                    fill="currentColor"
                    class="absolute top-0 left-0 z-0 hidden w-32 -mt-8 -ml-20 text-blue-gray-100 lg:w-32 lg:-ml-28 lg:-mt-10 sm:block"
                  >
                    <defs>
                      <pattern
                        id="e77df901-b9d7-4b9b-822e-16b2d410795b"
                        x="0"
                        y="0"
                        width=".135"
                        height=".30"
                      >
                        <circle cx="1" cy="1" r=".7"></circle>
                      </pattern>
                    </defs>
                    <rect
                      fill="url(#e77df901-b9d7-4b9b-822e-16b2d410795b)"
                      width="52"
                      height="24"
                    ></rect>
                  </svg>
                  <span class="relative">The</span>
                </span>
                Mew shop, lets get every things your mew want.
              </h2>
              <p class="text-base text-gray-700 md:text-lg">
                "What you wear is how you present yourself to the world,
                especially today, when human contacts are so quick. Fashion is
                instant language." —Miuccia Prada
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div>
      <div class="container text-center p-50">
        <div class="row">
          <h2
            class="text-center max-w-lg mb-6 font-sans text-3xl font-bold leading-none tracking-tight text-gray-900 sm:text-4xl md:mx-auto"
          >
            Products
          </h2>
        </div>

        <div class="row flex p-10 bg-white">
          <div
            class="card px-10 p-10 hover:shadow-xl duration-3 size-105"
            v-for="product in products"
            :key="product.id.toString()"
          >
            <div>
              <img :src="product.img" alt="">
              {{ product.name }}
              <div class="card">Price: {{ product.price }}</div>

              <button
                v-if="!product.cart"
                @click="add(product)"
                href="#"
                class="bg-purple-500 p-5 text-white"
              >
                Add to Cart
              </button>
              <button
                v-if="product.cart"
                @click="add(product)"
                :disabled="product.cart"
                href="#"
                class="bg-purple-200 p-5 text-gray-900 bodered"
              >
                Product Added to Cart
              </button>
            </div>
          </div>
        </div>
      </div>

      <div class="row">
        <div
          class="flex flex-col text-base text-gray-700 md:text-lg text-center"
        >
          <h2>Shopping Cart</h2>
        </div>
      </div>
      <table style="margin-left: 500px">
        <thead class="flex px-10 text-center">
          <td class="p-5">#</td>
          <td class="p-5">Quantity</td>
          <td class="p-5">Price</td>
          <td class="p-5">Product Name</td>
        </thead>
        <tbody>
          <tr v-for="(p, idx) in cart" :key="p.id.toString()" class="flex p-5">
            <td class="p-5">{{ idx + 1 }}</td>
            <td class="flex flex-inline">
              <button
                class="bg-green-500 p-5 text-white flex-1"
                @click="increment(p.id)"
              >
                +
              </button>
              <div class="flex flex-2 pt-5 p-3">{{ p.quantity }}</div>
              <button
                class="bg-red-500 p-5 text-white flex-3"
                @click="decrement(p.id)"
              >
                -
              </button>
            </td>
            <td class="p-5">{{ p.price }}</td>
            <td class="p-5">{{ p.name }}</td>
          </tr>
        </tbody>
      </table>

      <div>
        <h4 class="text-center">Total : {{ total }}</h4>
        <button></button>
      </div>
    </div>
  </div>
</template>

<script lang="js">
  export default {
    name: "Cart",
    props: {
      msg: String,
    },
    data() {
      return {
        ticket: {
          products: null,
          total: 0,
        },
        counter: 0,
        products: [
          {
            id: 1,
            img: require('@/assets/cat_cowboy.jpg'),
            name: "PETSIN 1pc Pirate Pet Costume & 1pc Pet Hat",
            price: 9.99,
            cart: false,
            quantity: 1,
          },
          {
            id: 2,
            img: require('@/assets/cat_doctor.jpg'),
            name: "PETSIN Doctor Design Pet Costume",
            price: 10.99,
            cart: false,
            quantity: 1,
          },
          {
            id: 3,
            img: require("@/assets/cat_maid.jpg"),
            name: "PETSIN Maid Design Pet Costume",
            price: 19.99,
            cart: false,
            quantity: 1,
          },
          {
            id: 4,
            img: require("@/assets/cat_pineapple.jpg"),
            name: "PETSIN Pineapple Design Pet Costume",
            price: 9.99,
            cart: false,
            quantity: 1,
          },
        ],
        cart: [],
        fields: ["#", "remove", "name", "quantity", "price"],
      }; // data return
    },
    methods: {
      add(product) {
        this.products[product.id - 1].cart = true;
        this.cart.push(product);
        // this.counter++;

      },
      increment(id) {
        const idx = this.cart.findIndex(c => c.id === id)
        this.cart[idx].quantity++

      },
      decrement(id) {
        const idx = this.cart.findIndex(c => c.id === id)
        if (this.cart[idx].quantity <= 0) return
        this.cart[idx].quantity--
      },
      buy() {
        alert("Purchase Complete");
      },
    },
    computed: {
      total() {
        let t = 0;
        for (let index = 0; index < this.cart.length; index++) {
          t += this.cart[index].price * this.cart[index].quantity;
        }
        return t.toFixed(2);
      },
    },
  }
</script>
