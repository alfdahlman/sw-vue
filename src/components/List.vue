<template>
  <div class="list">
    <ListItem
      v-for="( movie, index ) in movies"
      :key="index"
      :movie="movie"
      v-on="$listeners"
    />
  </div>
</template>

<script>
import ListItem from './subcomponents/ListItem.vue';

export default {
  name: 'List',
  components: {
    ListItem,
  },
  props: {
    movies: {
      type: Array,
      default: () => []
    },
  }
}
</script>

<style scoped>
  .list{
    width: 50%;
  }
</style>
