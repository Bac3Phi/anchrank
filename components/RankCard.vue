<template>
  <section>
    <div class="card rank-card">
      <header class="card-header">
        <p class="card-header-title has-text-grey">
          Marshal
        </p>
      </header>
      <div class="card-content">
        <div class="content has-text-centered" >
          <img src="https://acnhapi.com/v1/icons/villagers/372">
        </div>
      </div>
      <footer class="card-footer">
        <div class="card-footer-item">
          <slot />
        </div>
      </footer>
    </div>
  </section>  
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    icon_uri: {
      type: String
    },
    image_uri: {
      type: String
    },
    voted: {
      type: Number
    }
  },
}
</script>

<style lang="scss">
  .rank-card{
    width: auto;
  }

</style>