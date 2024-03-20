<template>
  <div class="item-list">
    <div v-for="(item, index) in items" :key="index" class="item">
      <div class="item-details">
        <p class="item-name ">{{ item.name }} : ${{ item.price }}</p>
      </div>
      <div class="button-group">
        <button @click="addToCart(item)" class="add-to-cart-btn">ADD TO CART</button>
        <button @click="updateItem(index)" class="update-btn">UPDATE</button>
        <button @click="removeItem(index)" class="remove-btn">REMOVE</button>
      </div>
    </div>
    <br>

  </div>
  <button @click="addItem" class="add-item-btn" style="float: right;">Add New Item</button>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { name: 'Product 1', price: 10 },
        { name: 'Product 2', price: 20 },
        { name: 'Product 3', price: 15 },
        { name: 'Product 4', price: 11 },
        { name: 'Product 5', price: 32 },
        { name: 'Product 6', price: 23 },

      ]
    };
  },
  methods: {
    addToCart(item) {
      this.$emit('add-to-cart', item);
    },
    updateItem(index) {
      const item = this.items[index];
      const newName = prompt('Enter the new name:', item.name);
      const newPrice = parseFloat(prompt('Enter the new price:', item.price));

      if (newName && !isNaN(newPrice)) {
        item.name = newName;
        item.price = newPrice;
      }
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
    addItem() {
      const name = prompt('Enter the name for the new item:');
      const price = parseFloat(prompt('Enter the price for the new item:'));

      if (name && !isNaN(price)) {
        this.items.push({ name, price });
      }
    }
  }
};
</script>



<style scoped>
.item-list {
  display: flex;
  flex-direction: column;
  align-items: center;

}



.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1px;
  border-bottom: 1px solid #ccc;
  width: 100%;

}

.item-details {
  flex: 1;
}

.item-name {
  padding: 2rem;
  margin: 0;
  font-weight: bold;
  color: #be4545;
}


.button-group {
  display: flex;
  gap: 10px;
}


.remove-btn{
  background-color: #be4545;
  border: none;
  border-radius: 20px;

}
.update-btn{
  background-color: #ebdc5b;
  border: none;
  border-radius: 20px;
  padding: 10px;  
}

.add-to-cart-btn{
  background-color: #4caf50;
  border: none;
  border-radius: 20px;
  padding: 10px; 
}


.add-item-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  
}


.add-item-btn:hover {
  background-color: #036796;
}
</style>
