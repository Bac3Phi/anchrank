<template>
  <section class="section">
    <div v-if="!Object.keys(this.data).length">
      <Skeleton />
    </div>
    <b-table :data="data" striped bordered v-else>
      <template slot-scope="props">
        <b-table-column field="id" label="ID" width="40" numeric>
          {{ props.row.id }}
        </b-table-column>
        <b-table-column field="icon_uri" label="Avatar">
          <img :src="props.row.icon_uri" />
        </b-table-column>
        <b-table-column field="name" label="Name" sortable searchable>
          {{ props.row.name }}
        </b-table-column>
        <b-table-column field="personality" label="Personality" sortable searchable>
          {{ props.row.personality }}
        </b-table-column>
        <b-table-column field="voted" label="Voted" sortable>
          {{ props.row.voted }}
        </b-table-column>
        <b-table-column field="rank" label="Rank" sortable searchable>
          <img :src="rank_url(props.row.rank)" :alt="props.row.rank"/>
        </b-table-column>
        <b-table-column label="Gender">
          {{ props.row.gender }}
        </b-table-column>
      </template>
    </b-table>
  </section>
</template>

<script>
import RankCard from "~/components/RankCard";
import axios from "axios";
import Skeleton from "~/components/Skeleton";

export default {
  name: "HomePage",

  components: {
    RankCard,
    Skeleton
  },
  data: function() {
    return {
      rank_meta: [
        {
          title: "1st",
          image_url: "~assets/medal-1.png"
        },
        {
          title: "2nd",
          image_url: "~assets/medal-2.png"
        },
        {
          title: "3rd",
          image_url: "~assets/medal-3.png"
        }
      ],
      data: [],
      columns: [
        {
          field: "id",
          label: "ID",
          width: "100",
          numeric: true,
          searchable: true
        },
        {
          field: "name",
          label: "Name",
          searchable: true
        },
        {
          field: "personality",
          label: "Personality",
          searchable: true
        },
        {
          field: "rank",
          label: "Rank",
          searchable: true
        },
        {
          field: "voted",
          label: "Point"
        },
        {
          field: "gender",
          label: "Gender"
        }
      ]
    };
  },
  mounted() {
    axios
      .get("https://acnhrank.herokuapp.com/api/v1/rankings")
      .then(response => {
        this.data = response.data;
      });
  },
  methods: {
    rank_url: (rank) => {
      var images = require.context('../assets/rank', false, /\.png$/)
      return images('./' + rank.toUpperCase() + ".png")
    }
  }
};
</script>
<style lang="scss">
.card-collection {
  width: 100%;
  .card-collection-content {
    background: white;
  }
}
.type-ssr {
  font-size: 30px;
  background: -webkit-linear-gradient(#eee, #333);
  -webkit-text-fill-color: transparent;
}
</style>
