<template>
  <div class="card">
    <header class="card-header">
      <div class="header-content">
        <div class="poster-details">
          🎁<span
            >Get a <b>{{ data.product }}</b> by
            <b>{{ data.poster.name }}</b></span
          >
        </div>
        <div class="right-content">
          <p class="subtitle is-7">
            <span class="is-7">{{ data.timestamp }}</span>
            <b-icon icon="clock" size="is-small"></b-icon>
          </p>
        </div>
      </div>
    </header>
    <div v-if="data.imgSrc" class="card-image">
      <figure class="image is-4by3">
        <img
          class="aspect-ratio-hack"
          :src="data.imgSrc"
          alt="Placeholder image"
        />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img
              :src="data.poster.imgSrc"
              alt="Placeholder image"
              style="object-fit: cover; border-radius: 5px;"
            />
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-4">{{ data.poster.name }}</p>
          <p class="subtitle is-6">{{ data.poster.info }}</p>
        </div>
      </div>
      <div class="content" v-html="data.content"></div>
    </div>
    <footer class="card-footer">
      <div class="card-footer-item">💰{{ data.price }}{{ data.unit }}</div>
      <div class="card-footer-item">
        <b-button type="is-primary" @click="displayError()">
          Buy Now
        </b-button>
      </div>
    </footer>
  </div>
</template>

<style scoped>
img.aspect-ratio-hack {
  object-fit: cover;
}
img.border-hack {
  border-radius: 10px 10px 0 0;
}
.card {
  border-radius: 5px;
  margin-bottom: 1.5rem;
}
.header-content {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 1rem;
}
.right-content {
  display: flex;
  align-items: center;
}
</style>

<script>
export default {
  props: ['data'],
  methods: {
    displayError: function() {
      this.$buefy.toast.open({
        duration: 1500,
        message: `Ooops. This is not yet implemented`,
        position: 'is-top',
        type: 'is-warning'
      })
    }
  }
}
</script>
