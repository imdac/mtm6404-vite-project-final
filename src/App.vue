<!-- Template (HTML) -->
<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <h1 class="display-4 py-4">Grocery List</h1>
      </div>
    </div>

    <div class="row">
      <div class="col">
        <ListGroup>
          <ListGroupItem 
            v-for="(item, index) in items" 
            :key="index"
            :index="index"
            :text="item.text"
            :initial-completed="item.completed"
            @update-item="updateItem"
            />
        </ListGroup>
      </div>
    </div>
  </div>
</template>


<!-- Logic (JS) -->
<script>
import ListGroupItem from './components/ListGroupItem.vue'
import ListGroup from './components/ListGroup.vue'

export default {
  name: 'App',
  components: { ListGroupItem, ListGroup },
  data: function () {
    return {
      items: [
        { text: 'Milk', completed: false }, // 0 
        { text: 'Bread', completed: true }, // 1
        { text: 'Eggs', completed: false } // 2
      ]
    }
  },
  created: function () {
    const items = localStorage.getItem('items')

    if (items) {
      this.items = JSON.parse(items)
    }
  },
  methods: {
    updateItem: function (index, completed) {
      this.items[index].completed = completed
    }
  },
  watch: {
    items: {
      deep: true,
      handler: function (items) {
        localStorage.setItem('items', JSON.stringify(items))
      }
    }
  }
}
</script>


<!-- Styles (CSS) -->
<style>
</style>