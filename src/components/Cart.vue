<template>
  <div class="row sticky-top">
    <div class="col-md-12">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">Commande</h5>
          <div class="card-text">
            <ul class="list-group">
              <li class="list-group-item"  v-for="product in cart" >
                {{ product.name }} - {{ product.quantity }}*{{ product.price }}$
                <button
                    class="btn btn-close btn-sm"
                  @click="removeItem(product)"  
                  />
              </li>
            </ul>
          </div>
        </div>

        <div class="row" v-if="cart.length > 0">
          <div class="d-grid col mx-3">
            <button class="btn btn-success" @click="isOrdered = !isOrdered">
              Commander
            </button>
          </div>
          <div class="d-grid col gap-2 py-2">Total: {{ totalPrice }}$</div>
        </div>

        <div class="row" v-else>
          <div class="col-md-12">
            <div class="alert alert-info">Votre panier est vide</div>
          </div>
        </div>

        <div class="row" v-if="isOrdered">
          <div class="col-md-12">
            <div class="card-body">
              <form @submit.prevent="order(orders)">
                <div class="form-group">
                  <input
                    type="text"
                    v-model="email"
                    class="form-control"
                    id="email"
                    name="email"
                    placeholder="Courriel"
                  />
                </div>
                <div class="form-group mt-2">
                  <button type="submit" class="btn btn-primary">
                    Soumettre
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["cart"],
  data() {
    return {
      isOrdered: false, // true quand on clique sur le bouton commander
      email: "",
    };
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, product) => {
        return total + product.price * product.quantity;
      }, 0);
    },
  },
  methods: {
    order(orders) {
      // Validation du courriel non vide et au format correct
      if (this.email.length > 0 && this.email.includes("@")) {
        this.$emit("order-cart", {
          email: this.email,
          cart: this.cart,
        });
        this.isOrdered = false;
        this.email = "";
      } else {
        alert("Courriel invalide");
      }
      // Envoi de la commande dans la base de données Firebase

      // "https://d10-ex-default-rtdb.europe-west1.firebasedatabase.app/orders.json"
      // Vous pouvez aussi utiliser votre propre base de données Firebase si vous en avez une
    fetch("https://d10-ex-default-rtdb.europe-west1.firebasedatabase.app/orders.json", {
      method: "POST",
      body: JSON.stringify([...this.cart, { email: this.email }]),
    })
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
          alert("Commande effectuée");
          this.cart.splice(0, this.cart.length);
          this.isOrdered = false;
          this.email = "";
    })
    .catch((error) => alert("il y a eu une erreur lors de votre commande"));
    },

    // Créer une fonction qui permet de supprimer un item du panier
    removeFromCart(item) {
      this.cart.splice(this.cart.indexOf(item), 1);
    },
  },
};
</script>

<style scoped></style>
