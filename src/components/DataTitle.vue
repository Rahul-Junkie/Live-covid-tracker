<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mt-4 mb-10 text-black">
      {{ timestamp }}
    </div>
  </div>
</template>
<script>
import moment from "moment";
export default {
  name: "DataTitle",
  props: ["text", "DataDate"],
  computed: {
    timestamp: function () {
      return moment(this.DataDate).format("MMMM Do YYYY,h:mm:s a");
    },
  },
};
</script>
