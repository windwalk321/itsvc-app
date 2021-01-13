<template>
  <nuxt-link
    class="list-item"
    :to="`/${item.id}`"
  >
    <img
      :src="item.image"
      :alt="item.name"
      class="list-item__img"
    >
    <span class="list-item__title">{{ item.name }}</span>
  </nuxt-link>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss">
.list-item {
  display: flex;
  flex-direction: column;
  cursor: pointer;
  text-decoration: none;
  background: rgb(60, 62, 68);
  border-radius: 0.5rem;
  overflow: hidden;
  &:hover &__title {
    color: rgb(255, 152, 0);
  }
  &__img {
    height: auto;
    max-width: 100%;
  }
  &__title {
    font-weight: bold;
    font-size: 1.2rem;
    letter-spacing: 0.01em;
    color: #fff;
    padding: 0.5rem;
  }
}
</style>
