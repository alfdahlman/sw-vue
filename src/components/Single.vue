<template>
  <div class="single">
    <div
      class="content"
      v-if="selected.fields"
    >
      <h2>{{ selected.fields.title }}</h2>
      <p>{{ selected.fields.opening_crawl }}</p>
      <p>Directed by: {{ selected.fields.director }}</p>
    </div>
    <div
      class="no-content"
      v-else
    >
      <p>No movie selected</p>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Single',
  props: {
    selected: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  .single{
    width: 50%;
    box-sizing: border-box;
    padding: 10px 30px;
    border-left: 1px solid grey;
    min-height: 500px;
  }

  .no-content{
    display: flex;
    height: 100%;
    align-items: center;
    justify-content: center;
  }
</style>
