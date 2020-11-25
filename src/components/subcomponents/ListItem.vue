<template>
  <div
    class="list-item"
    @click="$emit('onSelectMovie', movie.id)"
  >
    <p class="episode">EPISODE {{ movie.fields.episode_id }}</p>
    <p class="title">{{ movie.fields.title }}</p>
    <p class="date">{{ movie.fields.release_date }}</p>
  </div>
</template>

<script>
export default {
  name: 'ListItem',
  props: {
    movie: {
      type: Object,
      required: true
    }
  },
}
</script>

<style scoped>
  .list-item{
    border-bottom: 1px solid grey;
    cursor: pointer;
    transition: background-color .2s;
  }

  .list-item:hover{
    background-color: #F5F5F5;
  }

  P{
    display: inline-block;
    margin: 0;
    padding: 10px 15px;
  }

  .episode{
  }
  .title{
  }
  .date{
    float: right;
  }
</style>
