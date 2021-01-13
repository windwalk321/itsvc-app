<template>
  <div class="character">
    <span
      v-if="isLoading"
      class="character__preloader"
    >Loading...</span>
    <div
      v-else
      class="character__wrapper"
    >
      <img
        :src="character.image"
        :alt="character.name"
        class="avatar"
      >
      <div class="info">
        <div class="info__section">
          <h2 class="name">
            {{ character.name }}
          </h2>
          <div class="status">
            <div :style="{background: currentStatusColor}" class="status__icon" />
            <span class="status__text">{{ character.status }} - {{ character.gender }}</span>
          </div>
        </div>
        <div class="info__section">
          <span class="desc">Last known location:</span>
          <span class="value">{{ character.location.name }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      character: {},
      isLoading: true
    }
  },
  computed: {
    currentStatusColor () {
      const colors = {
        Alive: 'rgb(85, 204, 68)',
        Dead: 'rgb(214, 61, 46)',
        unknown: 'rgb(128,128,128)'
      }

      return colors[this.character.status]
    }
  },
  async mounted () {
    await this.$axios
      .get(`/character/${this.$route.params.character}`)
      .then((response) => {
        this.character = response.data
        this.isLoading = false
      })
      .catch(error => (console.log(error)))
  }
}
</script>

<style lang="scss">
.character {
  background: rgb(60, 62, 68);
  color: #fff;
  padding: 1rem;
}
.character__wrapper {
  display: flex;
  @media (max-width: 576px) {
    flex-direction: column;
  }
  .avatar {
    height: auto;
    max-width: 100%;
  }
  .info {
    display: flex;
    flex-direction: column;
    padding: 0 0 0 1rem;
    @media (max-width: 576px) {
      flex-direction: column;
      padding: 0;
    }
    &__section {
      display: flex;
      flex-direction: column;
      &:not(:last-child) {
        margin: 0 0 0.8rem 0;
      }
      .status {
        display: flex;
        align-items: center;
        &__icon {
          width: 0.5rem;
          height: 0.5rem;
          margin: 0 0.3rem 0 0;
          border-radius: 50%;
        }
        &__text {
          font-weight: 500;
        }
      }
      .desc {
        color: rgb(158, 158, 158);
        font-weight: 500;
      }
      .value {
        font-size: 1.2rem;
      }
    }
  }
}
</style>
