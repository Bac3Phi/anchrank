<template>
  <div class="card">
    <header class="card-header">
      <p class="card-header-title has-text-grey">
        {{ title }}
      </p>
    </header>
    <div class="card-content">
      <div class="content has-text-centered" >
        <b-tooltip :label="catch_phrase" always>
          <img
            :src="icon_uri"
            :style="{ width: 100 }"
            @click="isCardModalActive = true"
            style="cursor: pointer;"
          />
        </b-tooltip>
      </div>
      <b-tag rounded class="voted-group" size="is-large" type="is-white">
        <button v-on:click="vote('up')">
          <b-icon icon="arrow-up-thick" type="is-success"  />
       </button>
        <span>{{score}}</span>
        <button v-on:click="vote('down')">
          <b-icon icon="arrow-down-thick" type="is-danger" />
        </button>
      </b-tag>
    </div>
    <footer class="card-footer">
      <div class="card-footer-item">
        <slot />
      </div>
    </footer>
    <b-modal :active.sync="isCardModalActive" :width="256" :heigth="256" scroll="keep">
      <p class="image is-4by4">
        <img :src="image_uri">
      </p>
    </b-modal>
  </div>
</template>

<script>
import VueCookies from 'vue-cookies'
import axios from "axios";
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
    catch_phrase: {
      type: String
    },
    voted: {
      type: Number
    }
  },
  data(){
    return{
      isCardModalActive: false,
      voteType: 0,
      score: this.voted
    }
  },
  methods: {
    vote(voted_type){
      let voted_count = Number($cookies.get('voted_count'))
      if(voted_count < 20){
        $cookies.set('voted_count', voted_count += 1, "30min");
        this.score += voted_type === 'up' ? +1 : -1;

        axios
          .put(`https://acnhrank.herokuapp.com/api/v1/villagers/${this.id}`,{
            'voted_type': voted_type
          })
          .then(response => {
            this.villagers = response.data;
          });
      } else{
        this.$buefy.snackbar.open(`You have used up 20 votes, please come back in 30 minutes`)
      }
    },
  }
};
</script>
<style lang="scss">
  .card-content{
    position: relative;
  }
  .voted-group{
    height: 35px;
    position: absolute;
    right: 10px;
    bottom: -20px;
    background-color: white;
    border: 1px solid #dfe1e5;

    button{
      border: none;
      background-color: transparent;
      outline: none;
      cursor: pointer;
    }
  }
</style>