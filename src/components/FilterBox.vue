<template>
  <div
    :class="`${filters} filter-item`"
    :style="{ backgroundImage: `url(${imgUrl})` }"
    @click="$emit('clickFilter', filters)"
  >
    <slot name="filterName"
      ><span>{{ filters }}</span></slot
    >
  </div>
</template>

<script>
export default {
  name: "FilterBoxComponent",
  props: {
    imgUrl: String,
    filters: Array,
  },
};
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
  background-position: center;
}
</style>
