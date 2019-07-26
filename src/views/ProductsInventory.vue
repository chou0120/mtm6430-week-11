<template>
  <div>
    <h1>Products Inventory</h1>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Title</th>
          <th scope="col">Price</th>
          <th scope="col">Quantity</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.title }}</td>
          <td>{{ product.price }}</td>
          <td>
            <input type="number" min="0" v-model="product.quantity"/>
          </td>
          <td>
            <button class="btn btn-warning" @click="sendQuantity(product.quantity, product)">Add</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import { mapState } from "vuex";
import { mapActions } from "vuex";
export default {
  computed: {
     created() {
    this.$store.dispatch("fetchData");
  },
    ...mapState(["products"])
    // newComputed() {}
  },
  methods:{
    ...mapActions(["updateQuantity"]),
    sendQuantity(quantity, product) {
      // send the quantity to store and update the state and database
      if(quantity >=0 ){
      this.updateQuantity({quantity:quantity, product:product});
    }
    else{
      console.log("quantity must be 0 or above")
    }
  }
  }
};
</script>
