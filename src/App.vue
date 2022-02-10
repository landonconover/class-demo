<template>
<h1>Shopping list</h1>
  <ShoppingListForm @add:item='addItem' />
  <ShoppingList 
  @delete:item='deleteItem'
  @edit:item='editItem'
  :items='shoppingItems' />
</template>

<script>
import ShoppingList from './components/ShoppingList.vue'
import ShoppingListForm from './components/ShoppingListForm.vue'

export default {
  name: 'App',
  components: {
    ShoppingList,
    ShoppingListForm
  },
  data() {
    return {
      shoppingItems: [
        {
          id: 1,
          name: 'Jelly',
          amount: 1,
        },
        {
          id: 2,
          name: 'Peanut Butter',
          amount: 3,
        },
        {
          id: 3,
          name: 'Bread',
          amount: 1,
        },
        {
          id: 4,
          name: 'mustard',
          amount: 1,
        },
      ]
    }
  },
  methods: {
    addItem(item) {
      //make an id too
      const lastId = this.shoppingItems.length > 0
      ? this.shoppingItems[this.shoppingItems.length -1].id
      : 0;

      const id = lastId + 1;

      const newItem = { ...item, id}

      this.shoppingItems = [ ...this.shoppingItems, newItem]
    },
    deleteItem(id) {
      this.shoppingItems = this.shoppingItems.filter(item => item.id !== id)
    },
    editItem(id, updatedItem) {
      this.shoppingItems = this.shoppingItems
        .map(item => {
          return item.id === id ? updatedItem : item
        })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
