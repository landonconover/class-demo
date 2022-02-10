<template>
  <div id="shoppinglist-table">
      
      <table>
      <thead>
        <tr>
          <th>Item</th>
          <th>Amount</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key='item.id'>
            <td v-if="editing === item.id">
                <input type="text" v-model="item.name">
            </td>
            <td v-else>{{item.name}}</td>

            <td v-if="editing === item.id">
                <input type="text" v-model="item.amount">
            </td>
            <td v-else>{{item.amount}}</td>
          
            <td v-if="editing === item.id">
            <button @click="editItem(item)">Save</button>
            <button class='muted-button' @click="editing = null">Cancel</button>
            </td>
            <td v-else>
                <button @click="editMode(item.id)">Edit</button>
                <button @click="$emit('delete:item', item.id)">Delete</button>
            </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
    name: 'shopping-list',
    props: {
        items: Array
    },
    data() {
        return {
            editing: null
        }
    },
    methods: {
        editMode(id) {
            this.editing = id
        },
        editItem(item) {
            //check for blank vals
            if(item.name === '' || item.amount === '') return

            //otherwise emit the vals to the parent and clear edit mode
            this.$emit('edit:item', item.id, item)
            
            this.editing = null
        }
    }
}
</script>

<style scoped>

</style>