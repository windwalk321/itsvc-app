<template>
  <div class="app">
    <span
      v-if="isLoading"
      class="app__preloader"
    >Loading...</span>
    <div
      v-else
      class="app__items"
    >
      <list-item
        v-for="item in characters"
        :key="item.id"
        :item="item"
      />
    </div>
    <infinite-loading
      spinner="spiral"
      @infinite="infiniteScroll"
    />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      characters: [],
      isLoading: true,
      page: 1
    }
  },
  async mounted () {
    await this.$axios
      .get(`/character/?page=${this.page}`)
      .then((response) => {
        this.characters = response.data.results
        this.isLoading = false
      })
      .catch(error => (console.log(error)))
  },
  methods: {
    infiniteScroll ($state) {
      setTimeout(() => {
        this.page++
        this.$axios
          .get(`/character/?page=${this.page}`)
          .then((response) => {
            console.log(response)
            if (response.data.results.length > 1) {
              this.characters = [...this.characters, ...response.data.results]
              $state.loaded()
            } else {
              $state.complete()
            }
          })
          .catch((error) => {
            console.log(error)
          })
      }, 500)
    }
  }
}
</script>

<style lang="scss">
.app {
  &__items {
    display: grid;
    grid-gap: 1rem;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  }
}
</style>
