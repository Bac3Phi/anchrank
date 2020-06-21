<template>
  <div class="card">
    <header class="card-header">
      <p class="card-header-title has-text-grey">
        {{ title }}
      </p>
    </header>
    <div class="card-content">
      <div class="content has-text-centered">
        <b-tooltip :label="catch_phrase" always>
          <img :src="icon_uri" :style="{ width: 100 }">
        </b-tooltip>
      </div>
    </div>
    <footer class="card-footer">
      <div class="card-footer-item">
        <slot />
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    icon_uri: {
      type: String
    },
    catch_phrase: {
      type: String
    }
  }
}
</script>
