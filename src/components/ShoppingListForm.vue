<template>
    <div id="shopping-form">
    <form @submit.prevent='handleSubmit'>
      <label>Shopping Item</label>
      <input v-model="item.name" type="text" />
      <label>Item Amount</label>
      <input v-model="item.amount" type="number" />
      <button>Add item</button>
    </form>
  </div>
</template>

<script>
export default {
    name: 'shopping-form',
    data() {
      return {
        item: {
          name: '',
          amount: '',
        },
      }
    },
    methods: {
        handleSubmit() {
            this.$emit('add:item', this.item)
            this.item = {
                name: '',
                amount: '',
            }
        }
    }
}
</script>

<style>
form {
    margin-bottom: 2rem;
  }
</style>