<script>
import { RouterView } from "vue-router";
import { ref } from "vue";
import axios from "axios";

export default {
  data() {
    return {
      cari:null,
      error: false,
      loading: true,
      juzs: ref([]),
      surahs: ref([]),
    };
  },
  components: {
    RouterView,
  },

  mounted() {
    this.getJuz();
    this.getSurah();
  },
  methods: {
    getJuz() {
      axios
        .get("https://api.quran.com/api/v4/juzs")
        .then((response) => {
          this.juzs = response.data.juzs;
        })
        .catch((error) => {
          console.log(error);
          this.error = true;
        })
        .finally(() => (this.loading = false));
    },
    getSurah() {
      axios
        .get("https://api.quran.com/api/v4/chapters")
        .then((response) => {
          this.surahs = response.data.chapters;
        })
        .catch((error) => {
          console.log(error);
          this.error = true;
        })
        .finally(() => (this.loading = false));
    },
  },
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light" style="position: fixed; top: 0; width: 100%" id="navbar">
    <div class="container">
      <a class="navbar-brand text-white" href="#" > My Quran</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse " id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link active text-white" to ="/">Home</router-link>
          </li>
        </ul>
        <li class="nav dropdown">
          <a
            class="nav-link dropdown-toggle text-white"
            data-bs-toggle="dropdown"
            href="#"
            role="button"
            aria-expanded="false">Juz</a>=
          <ul class="dropdown-menu">
            <li v-for="juz in juzs" :key="juz.id">
              <router-link
                :to="{ name: 'juzs', params: { id: juz.id } }"
                class="dropdown-item"
                >{{ juz.juz_number }}</router-link>
            </li>
          </ul>
        </li>

        <li class="nav dropdown">
          <a
            class="nav-link dropdown-toggle text-white"
            data-bs-toggle="dropdown"
            href="#"
            role="button"
            aria-expanded="false">Info Surah</a>
          <ul class="dropdown-menu">
            <li v-for="surah in surahs" :key="surah.id">
              <router-link
                :to="{ name: 'surahs', params: { id: surah.id } }"
                class="dropdown-item"
                >{{ surah.name_complex }}</router-link>
            </li>
          </ul>
        </li>
        <ul class="navbar-nav text-lg-end">
          <li class="nav-item">
            <router-link class="nav-link active text-white" to ="/about">About</router-link>
          </li>
        </ul>
      </div>
      <RouterView />
    </div>
  </nav>

</template>

<style>
.navbar{
  background: linear-gradient(50deg, #08084b, #5e5e9d);
  animation: hue-rotate 5s linear infinite alternate;
  border-color: white;
}
@keyframes hue-rotate {
  to{filter: hue-rotate(90deg);}
}
</style>