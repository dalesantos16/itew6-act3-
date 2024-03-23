<template>
  <div class="cart">
    <!-- Cart items -->
    <div v-for="(item, index) in cart" :key="index" class="cart-item">
      <div class="item-details">
        <p class="item-name">{{ item.name }} : ${{ item.price }}</p>
        <p class="item-quantity">Quantity: {{ item.quantity }}</p>
      </div>
      <div class="quantity-controls">
        <button @click="openDialog(index)" class="btn_update">UPDATE</button>
        <button @click="removeFromCart(index)" class="btn_delete">REMOVE</button>
      </div>
    </div>

    <!-- Total -->
    <p class="total">Total: $ {{ total }}</p>

    <!-- Dialog for updating quantity -->
    <div v-if="dialogVisible" class="dialog">
      <div class="dialog-content">
        <p>Enter new quantity for {{ cart[selectedItemIndex].name }}:</p>
        <input type="number" v-model="newQuantity" @keydown.enter="updateQuantity(selectedItemIndex)">
        <button @click="updateQuantity(selectedItemIndex)">Save</button>
        <button @click="closeDialog">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false,
      selectedItemIndex: null,
      newQuantity: '', 
    };
  },
  props: {
    cart: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    total() {
      if (this.cart.length === 0) {
        return 0; 
      }
      return this.cart.reduce((acc, item) => acc + item.price * item.quantity, 0);
    },
  },
  methods: {
    openDialog(index) {
      this.selectedItemIndex = index;
      this.newQuantity = this.cart[index].quantity.toString(); 
      this.dialogVisible = true;
    },
    closeDialog() {
      this.dialogVisible = false;
    },
    updateQuantity(index) {
      const newQuantity = parseInt(this.newQuantity);
      if (!isNaN(newQuantity) && newQuantity >= 0) {
        
        this.$emit('update-quantity', { index, quantity: newQuantity });
        this.closeDialog();
        alert("Successfully Updated");
      } else {
        alert('Please enter a valid non-negative integer!');
      }
    },
    removeFromCart(index) {
      const validation = confirm("Are you sure you want to remove?");

      if(validation == true)
      {
        alert("Successfully Removed!");
        this.$emit('remove-from-cart', index);
      } else {
        return;
      }      
    },
  },
};
</script>

<style scoped>

.cart {
  margin-top: 20px;
}

.cart-item {
  text-align: center;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 10px;
}

.item-details {
  flex: 1;
}

.item-name {
  margin: 0;
  font-weight: bold;
}

.btn_update {
  margin-top: 13px;
  margin-left: 45%;
  font-family:'Franklin Gothic Medium';
  font-size: 90%;
  padding: 20px 20px;
  background-color: yellow;
  border: none;
  border-radius: 20px;
  padding: 10px;
  color: rgb(206, 64, 64);
  box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);
}

.btn_delete {
  margin-top: 15px;
  font-family:'Franklin Gothic Medium';
  font-size: 90%;
  padding: 20px 20px;
  background-color: rgb(179, 96, 96);
  border: none;
  border-radius: 20px;
  padding: 10px;
  color: white;
  box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);
}

.item-quantity {
  margin: 0;
}

.item-price {
  margin: 0;
}

.quantity-controls {
  display: flex;
  align-items: center;
}

button {
  margin-left: 10px;
}

.total {
  border: 5px solid #080808;
  border-radius: 10px;
  font-size: 18px;
  font-weight: bold;
  margin-top: 20px;
  background-color: rgb(240, 198, 148);
  padding: 20px;
  text-align: center;
  
}

.dialog {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.dialog-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
}

.dialog-content input {
  width: 100px;
}
</style>
