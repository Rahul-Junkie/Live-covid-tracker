<template>
  <main v-if="!loading">
    <data-title :text="title" :DataDate="dataDate" />
    <data-boxes :stats="stats" />
    <Country @get-country="countryData" :countries="countries" />
    <button
      class="
        bg-green-700
        text-white
        rounded
        p-3
        mt-10
        mb-10
        focus:outline-none
        hover:bg-green
      "
      @click="clear"
      v-if="stats.Country"
    >
      Clear Data
    </button>
  </main>
  <main v-else class="flex-col align-center justify-center text-center">
    <div class="text-grey-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImg" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
// @ is an alias to /src
import DataTitle from "../components/DataTitle.vue";
import DataBoxes from "../components/DataBoxes.vue";
import Country from "../components/Country.vue";
export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    Country,
  },
  data() {
    DataTitle;
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImg: require("../assets/covid.gif"),
    };
  },
  methods: {
    get_data() {
      fetch("https://api.covid19api.com/summary")
        .then((response) => response.json())
        .then(
          (data) => (
            (this.loading = false),
            (this.dataDate = data.Date),
            (this.stats = data.Global),
            (this.countries = data.Countries)
          )
        );
    },
    clear() {
      this.loading = true;
      this.$router.go(this.$router.currentRoute);
    },
    countryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
  },
  created() {
    this.get_data();
  },
};
</script>
