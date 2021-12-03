<template>
  <div class="container-fluid mt-5">
    <div style="text-align: center">
      <h1>Bienvenidos a mi verdurería :u</h1>
    </div>
    <p>
      Buenas, buenas... mi doña! Siga sin compromiso y mire los precios de nuestros productos.<br>
      Aproveche que la verdura está fresquita y se acaba rapidito.  Venga, tómese un tintico :v...
    </p>
    <Products 
    :products="products"
    v-on:addItem="onAddedItem"
    v-on:removeItem="onDeletedItem"
    :disableButton="disableRemoveItem"/>
    <hr>
    <ShoppingList :itemsList="itemsList"/>
  </div>
</template>

<script>
import Products from './components/Products.vue'
import ShoppingList from './components/ShoppingList.vue'

export default {
  name: 'App',
  components: {
    Products,
    ShoppingList
  },
  data() {
    return {
      products: [{
        id: 1,
        name: "Plátano verde",
        price: 1000,
        image: "https://organicosysaludables.com/wp-content/uploads/2021/03/Platano-verde-organico-certificado.jpg",
        stock: 10
      }, {
        id: 2,
        name: "Papa",
        price: 3000,
        image: "https://agro.bayer.co/-/media/bcs-inter/ws_colombia/cultivos/papa/papa.png",
        stock: 5
      }, {
        id: 3,
        name: "Zanahoria",
        price: 1800,
        image: "https://www.cocinayvino.com/wp-content/uploads/2016/09/zanahorias2.jpg",
        stock: 7
      }],
      itemsList: []
    }
  },
  methods: {
    onAddedItem(name) {
      const index = this.itemsList.findIndex(item => item.name == name);
      const pIndex = this.products.findIndex(item => item.name == name);
      this.products[pIndex].stock -= 1;
      if (index < 0) {
        this.itemsList.push({
          ...this.products[pIndex],
          image: undefined,
          stock: undefined,
          quantity: 1,
          total: this.products[pIndex].price * 1
        });
      } else {
        this.itemsList[index].quantity += 1;
        this.itemsList[index].total = this.itemsList[index].quantity * this.itemsList[index].price;
      }
    },
    onDeletedItem(name) {
      const index = this.itemsList.findIndex(item => item.name == name);
      const pIndex = this.products.findIndex(item => item.name == name);
      if (index >= 0) {
        this.itemsList[index].quantity -= 1;
        this.products[pIndex].stock += 1;
        if (this.itemsList[index].quantity <= 0) {
          this.itemsList.splice(index, 1);
        } else {
          this.itemsList[index].total = this.itemsList[index].quantity * this.itemsList[index].price;
        }
      }
    },
    disableRemoveItem(name) {
      return this.itemsList.findIndex(item => item.name == name) < 0;
    }
  }
}
</script>

<style>

</style>
