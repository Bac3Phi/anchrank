<template>
  <section class="section">
    <div class="capu-form-input">
      <strong>1st</strong>
      <v-select :options="options">
        <template v-slot:option="option">
          <img :src="option.icon_uri" />
          {{ option.name }}
        </template>
      </v-select>
    </div>
    <div class="capu-form-input">
      <strong>2nd</strong>
      <v-select :options="options">
        <template v-slot:option="option">
          <img :src="option.icon_uri" />
          {{ option.name }}
        </template>
      </v-select>
    </div>
    <div class="capu-form-input">
      <strong>3rd</strong>
      <v-select :options="options">
        <template v-slot:option="option">
          <img :src="option.icon_uri" />
          {{ option.name }}
        </template>
      </v-select>
    </div>
    <div class="buttons dudua-group">
      <b-button type="is-primary" expanded size="is-large"><b-icon icon="coffee-maker"/><strong>Take your Capuchino</strong></b-button>
    <img src="~assets/dudua.png">
    </div>
  </section>
</template>

<script>
import vSelect from "vue-select";
import "vue-select/dist/vue-select.css";
import axios from "axios";

export default {
  components: {
    vSelect
  },
  data: function() {
    return {
      options: []
    };
  },
  mounted() {
    axios
      .get("https://acnhrank.herokuapp.com/api/v1/villagers")
      .then(response => {
        this.options = response.data.map(obj => ({ ...obj, label: obj.name }));
      });
  }
};
</script>

<style>
.dudua-group{
  position: relative;
}

.dudua-group img{
  position: absolute;
  right: -19px;
  top: 42px;
}

.v-select .dropdown-toggle {
  display: flex !important;
  flex-wrap: wrap;
}

.v-select input[type="search"],
.v-select input[type="search"]:focus {
  flex-basis: 20px;
  flex-grow: 1;
  height: 50px;
  padding: 0 20px 0 10px;
  width: 100% !important;
}

.capu-form-input {
  margin-bottom: 20px;
}
</style>
