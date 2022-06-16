<template>
  <div class="row">
    <div class="col-md-8">
      <div class="row">
        <Product v-for="product in products" :key="product.id"
        :product="product"
        @add-to-cart="addToCart"
        />
      </div>
    </div>
    <div class="col-md-4 mt-5">
      <Cart :cart="cart" />
    </div>
  </div>
</template>

<script>
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";

export default {
  components: {
    Product,
    Cart,
  },
  data() {
    return {
      products: [], // tableau des pizzas
      cart: [], // tableau des pizzas dans le panier
    };
  },
  created() {
    this.getPizzas();
  },
  methods: {
    // Va chercher les pizzas depuis la base de données et les stocke dans le tableau products
    getPizzas() {
      fetch("https://d10-ex-default-rtdb.europe-west1.firebasedatabase.app/pizzas.json")
        .then((response) => response.json())
        .then((data) => {
          this.products = data;
        });

    },

    // Ajoute une pizza au panier (cart)
    // Cette méthode est exécutée lorsque l'utilisateur clique sur le bouton "Ajouter" à partir du composant Product.vue
    addToCart(product) {
      this.cart.push(product); 
    },
  },
};
</script>

<style scoped></style>
