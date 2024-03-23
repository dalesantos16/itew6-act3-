<template>
    <div id="app">
      <h1 style="text-align: center;">LIST</h1>
      <item-list @add-to-cart="addToCart"></item-list>
  
      <h1 style="text-align: center ; padding-top: 20px; padding-left: 160px; color: orange;">SHOPPING CART</h1>
      <shopping-cart :cart="cart" @update-quantity="updateQuantity" @remove-from-cart="removeFromCart"></shopping-cart>
  
      <button class="logout-button" @click="logout">LOGOUT</button>
    </div>
  </template>
  
  <script>
  import ItemList from './itemList.vue';
  import ShoppingCart from './shoppingCart.vue';
  
  export default {
    components: {
      ItemList,
      ShoppingCart
    },
    data() {
      return {
        cart: []
      };
    },
    methods: {
      addToCart(item) {
        const existingItemIndex = this.cart.findIndex(i => i.name === item.name);
        if (existingItemIndex !== -1) {
          this.cart[existingItemIndex].quantity++;
        } else {
          this.cart.push({ ...item, quantity: 1 });
        }
      },
      updateQuantity({ index, quantity }) {
        this.cart[index].quantity = quantity;
        if (this.cart[index].quantity <= 0) {
          this.cart.splice(index, 1);
        }
      },
      removeFromCart(index) {
        this.cart.splice(index, 1);
      },
      logout() {
        localStorage.removeItem('token');
        this.$router.push({ name: 'login' });
      }
    }
  };
  </script>
  
  <style scoped>
  
  .logout-button {
   float: right;
   font-family:'Franklin Gothic Medium';
   font-size: 30px;
    bottom: 20px;
    right: 20px;
    background-color: #ff5722;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
    box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);
  }
  
  .logout-button:hover {
    background-color: #e64a19;
  }

  .h1{
    align-items: center;
  }
  </style>
  