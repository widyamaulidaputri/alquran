<script>
import { ref } from "vue";
import axios from "axios";
import NavBar from "../components/NavBar.vue";

export default {
  components: {  NavBar },
  data() {
    return {
      error: false,
      loading: true,
      juzs: ref([]),
      ayat: ref([]),
    };
  },

  mounted() {
    this.getJuz();
    this.getAyat();
  },
  methods: {
    getJuz() {
      axios
        .get("https://api.quran.com/api/v4/juzs" + this.$route.params.id)
        .then((response) => {
          this.juzs = response.data.juzs;
        })
        .catch((error) => {
          console.log(error);
          this.error = true;
        })
        .finally(() => (this.loading = false));
    },
    getAyat() {
      axios
        .get(
          "https://api.quran.com/api/v4/quran/verses/uthmani?juz_number=" +
            this.$route.params.id
        )
        .then((response) => {
          this.ayat = response.data.verses;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(() => (this.loading = false));
    },
  },
};
</script>
<template>
  <NavBar />
  <div class="p text-center">
    <h4>Juz {{ $route.params.id }}</h4>
    <h5 v-for="isi in ayat" :key="isi.id" class="text-lg-end mt-5">
      {{ isi.text_uthmani }} {{ isi.verse_key }}
    </h5>
  </div>
</template>
<style scoped>
.p {
  font-family: Roboto;
}
</style>
