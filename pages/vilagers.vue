<template>
  <section class="section">
    <b-field>
      <b-input
        placeholder="Search..."
        type="search"
        icon="magnify"
        icon-clickable
        v-model="search"
      >
      </b-input>
    </b-field>
    <div v-if="!Object.keys(this.villagers).length">
      <Skeleton />
    </div>
    <div class="columns is-multiline is-mobile" v-else>
      <div
        v-for="villager in filteredList"
        v-bind:key="villager.id"
        class="column"
      >
        <card
          :id="villager.id"
          :title="villager.name"
          :icon_uri="villager.icon_uri"
          :catch_phrase="villager.catch_phrase"
          :image_uri="villager.image_uri"
          :voted="villager.voted"
          :rank="villager.rank"
        >
          <div class="w-100">
            <p>
              <strong>Gender: </strong><span>{{ villager.gender }}</span>
            </p>
            <p>
              <strong>Personality: </strong
              ><span>{{ villager.personality }}</span>
            </p>
            <p>
              <strong>Birthday: </strong><span>{{ villager.birthday }}</span>
            </p>
          </div>
        </card>
      </div>
    </div>
  </section>
</template>

<script>
import Card from "~/components/Card";
import Skeleton from "~/components/Skeleton";
import axios from "axios";

export default {
  name: "HomePage",

  components: {
    Card,
    Skeleton
  },
  data: function() {
    return {
      search: "",
      villagers: {}
    };
  },
  mounted() {
    axios
      .get("https://acnhrank.herokuapp.com/api/v1/villagers")
      .then(response => {
        this.villagers = response.data;
      });
  },
  computed: {
    filteredList() {
      return Object.values(this.villagers).filter(villager => {
        return (
          villager.name.toLowerCase().includes(this.search.toLowerCase()) ||
          villager.personality.toLowerCase().includes(this.search.toLowerCase())
        );
      });
    }
  }
};
</script>
