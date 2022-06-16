<template>
  <div class="col-md-6 col-sm-12">
    <div class="border bg-light mb-4">
      <div class="card-body">
        <!-- picture -->
        <div class="row">
          <div class="col-md-12">
            <img :src="product.picture" class="img-fluid" alt="" />
          </div>
        </div>
        <h5 class="card-title">{{ product.name }}</h5>
        <p class="card-text">{{ product.price }}$</p>
        <!-- row 2 cols -->
        <div class="row">
          <div class="col-md-8">
            <label  :class="{invalidQuantity}" >Quantité:
              <input type="number" v-model="quantity" min="0" max="10" />
            </label>
          </div>
          <div class="col-md-4">
            <button
              class="btn btn-primary"
              :class="{'btn-success': quantity > 0}"
              @click="addToCart()"
             
            >
              Ajouter
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  watch: {
    quantity(newValue) {
      if (newValue < 0) {
        this.invalidQuantity = true;
      } else {
        this.invalidQuantity = false;
      }
    },

  },
  data() {
    return {
      quantity: 0,
      invalidQuantity: false,
    };
  },
  methods: {
    addToCart() {
      // faire un emit avec l'événement add-to-cart
      // avec les données id, name, price, quantity
      this.$emit("add-to-cart", {
        id: this.product.id,
        name: this.product.name,
        price: this.product.price,
        quantity: this.quantity,
      });
    },
  },
 
};
</script>

<style scoped>
input {
  width: 70px;
}
.invalid {
  color: red;
}
</style>
