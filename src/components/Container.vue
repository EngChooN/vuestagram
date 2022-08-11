<template>
  <div>
    <Post v-for="(el, index) in boards" :key="index" :elBoards="el" />
  </div>
</template>

<script>
import Post from "./Post.vue";

export default {
  name: "ContainerComponent",
  components: {
    Post,
  },
  props: {
    boards: Array,
  },
};
</script>

<style></style>
