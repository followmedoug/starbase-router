<template>
  <div class="col-md-12">
    <Item v-for='(item, index) in items'
    :passed-item='item'
    :type= 'type' />
  </div>
</template>
<script>

import Item from './item.vue'

export default {
  data() {
    return {
      type: this.$route.params.type,
      items: []
    };
  },
  watch: {
    $route: "fechItems"
  },
  methods: {
    fechItems() {
      this.items = [];
      this.type = this.$route.params.type;
      let initial_ids = [2, 3, 4];

      for (let i in initial_ids) {
        let id = initial_ids[i];
        fetch(`https://swapi.co/api/${this.type}/${id}`, {
          method: "GET"
        })
          .then(response => response.json())
          .then(json => this.items.push(json));
      }
    }
  },
  created() {
    this.fechItems();
  },
  components: {
    Item
  }
};
</script>