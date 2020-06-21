<template>
  <div class="main">
    <b-navbar>
      <template slot="brand">
        <b-navbar-item tag="router-link" :to="{ path: '/' }">
          <img
            src="~assets/Blathers.png"
            alt="Lightweight UI components for Vue.js based on Bulma"
          />
        </b-navbar-item>
      </template>
      <template slot="start">
        <b-navbar-item v-for="(item, key) of items" :key="key">
          <nuxt-link :to="item.to" exact-active-class="is-active">
            <b-icon :icon="item.icon" /> {{ item.title }}
          </nuxt-link>
        </b-navbar-item>

      </template>

      <template slot="end">
        <b-navbar-item tag="div">
            <nuxt-link to="capuchino" class="button is-primary">
              <b-icon icon="coffee-to-go"/>
              <strong>Submit a Capuchino</strong>
            </nuxt-link>
            <!-- <a class="button is-light">
              Log in
            </a> -->

        </b-navbar-item>
      </template>
    </b-navbar>

    <section class="main-content columns">
      <div class="container">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: "Rank",
          icon: "crown-outline",
          to: { name: "index" }
        },
        {
          title: "Vilagers",
          icon: "home-variant-outline",
          to: { name: "vilagers" }
        },
        {
          title: "Chill",
          icon: "coffee",
          to: { name: "chill" }
        },
      ]
    };
  }
};
</script>

