<template>

  <div class="item-list">
    <div v-for="(item, index) in items" :key="index" class="item">
      <div class="item-details">
        <p class="item-name">{{ item.name }} : ${{ item.price }}</p>
      </div>
      <div class="button-group">
        <b>
          <button @click="addToCart(item)" class="add-to-cart-btn">ADD TO CART</button>   
          <button @click="updateItem(index)" class="update-btn">UPDATE</button>         
          <button @click="removeItem(index)" class="remove-btn">REMOVE</button>
        </b>
      </div>
    </div>
    <br>

  </div>
  <button @click="addItem" class="add-item-btn" style="float: right;">Add New Item</button> <br>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { name: 'CellPhone Stand', price: 50 },
        { name: 'Realme C10 CASE', price: 100 }
      ]
    };
  },
  methods: {
    addToCart(item) {     
        alert("Add to cart successfully!");
        this.$emit('add-to-cart', item);      
    },
    updateItem(index) {
      const item = this.items[index]; 
     
       const newName = prompt('Enter Product:', item.name);
       const newPrice = parseFloat(prompt('Enter Price:', item.price));
         
      if (newName && !isNaN(newPrice)) {
        item.name = newName;
        item.price = newPrice;
      }
    },
    removeItem(index) {
      const item = this.items[index];
      const validation = confirm("Are you sure you want to remove:\n            " + item.name);

      if(validation == true)
      {
        alert("Successfully Deleted!");
        this.items.splice(index, 1);
      }
      else 
      {
        return;
    }

    },
    addItem() {
      const name = prompt('Enter an Item:');
      const price = parseFloat(prompt('Enter Price:'));

      if(name == null || price == null){
        alert("Please Insert data!");
        return;
      }

      if (name && !isNaN(price)) {
        this.items.push({ name, price });
        alert("Successfully Added!");
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
  text-align: center;
  justify-content: space-between;
  align-items: center;
  padding: 4px;
  width: 100%;
  border: 3px solid #ccc;
  border-radius: 10px;
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
  margin-top: 13px;
  margin-left: 40%;
  display: flex;
  gap: 10px;
}


.remove-btn{  
  margin-left: 10px;
  font-family:'Franklin Gothic Medium';
  font-size: 90%;
  padding: 20px 20px;
  background-color: #be4545;
  border: none;
  border-radius: 20px;
  box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);

}
.update-btn{
  margin-left: 20px;
  font-family:'Franklin Gothic Medium';
  font-size: 15px;
  padding: 20px 60px;
  background-color: #ebdc5b;
  border: none;
  border-radius: 20px;
  padding: 10px;  
  box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);
  
}

.add-to-cart-btn{
  font-family:'Franklin Gothic Medium';
  font-size: 15px;
  padding: 10px 20px;
  background-color: #4caf50;
  border: none;
  border-radius: 20px;
  padding: 10px; 
  box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);
}


.add-item-btn {
  font-size: 20px;
  padding: 20px 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  box-shadow: 10px 10px 10px 0px rgba(0,0,0,0.5);
  
}


.add-item-btn:hover {
  background-color: #036796;
}
</style>
