<template>
  <div class="card">
    <header class="card-header">
      <div class="header-content">
        <div class="poster-details">
          📅<span class="has-text-weight-bold">{{ data.poster.name }}</span>
          uploaded a new project in <b>{{ data.location }}</b>
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
      <div class="progress-container">
        <div class="level">
          <div class="level-item level-left is-5">
            <div>
              <p class="heading">Backers</p>
              <p class="title is-6">{{ data.backers }}</p>
            </div>
          </div>
          <div class="level-item level-right">
            <div>
              <p class="heading">Raised</p>
              <p>
                <span class="title is-6">{{ data.covered }}</span
                ><span class="subtitle is-7"> of {{ data.goal }}€ goal</span>
              </p>
            </div>
          </div>
        </div>
        <b-progress type="is-primary" :value="percentLeft" show-value
          ><b-tooltip :label="percentLeft + '% left'" type="is-dark"
            >{{ data.covered }}€ of {{ data.goal }}€
          </b-tooltip></b-progress
        >
      </div>
    </div>
    <footer class="card-footer">
      <div class="card-footer-item">🕐 {{ data.deadline }} days left</div>
      <div class="card-footer-item">
        <b-button
          v-if="data.projectId"
          type="is-primary"
          tag="a"
          target="_blank"
          :href="'https://test.comgo.io/pages/ldg?projectId=' + data.projectId"
        >
          🤲 Donate
        </b-button>
        <b-button v-else type="is-primary" @click="displayError()">
          🤲 Donate
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
  computed: {
    percentLeft: function() {
      return Math.round((this.data.coveredNum / this.data.goalNum) * 100)
    }
  },
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
