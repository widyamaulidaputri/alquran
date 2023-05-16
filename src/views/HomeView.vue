<script>
import { ref } from "vue";
import axios from "axios";
import NavBar from "../components/NavBar.vue";

export default {
  components: {  NavBar },
  data() {
    return {
      cari: null,
      surah: ref([]),
      judul: ref([]),
      translation: ref([]),
      name: [],
      audio: ref([]),
    };
  },

  watch: {
    cari() {
      this.getSurah();
      this.getJudul();
      this.getTranslation();
      this.getAudio();
    },
  },

  mounted() {
    this.getSurah();
    this.getJudul();
    this.getTranslation();
    this.getAudio();
  },
  methods: {
    getSurah() {
      axios
          .get(
              "https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=" +
              this.cari
          )
          .then((response) => {
            this.surah = response.data.verses;
          })
          .catch((error) => {
            console.log(error);
          })
          .finally(() => (this.loading = false));
    },
    getJudul() {
      axios
          .get(
              "https://api.quran.com/api/v4/chapters/" + this.cari + "?language=id"
          )
          .then((response) => {
            this.judul = response.data.chapter;
            this.name = this.judul.translated_name;
          })
          .catch((error) => {
            console.log(error);
          })
          .finally(() => (this.loading = false));
    },
    getTranslation() {
      axios
          .get(
              "https://api.quran.com/api/v4/quran/translations/39?chapter_number=" +
              this.cari
          )
          .then((response) => {
            this.translation = response.data.translations;
          })
          .catch((error) => {
            console.log(error);
          })
          .finally(() => (this.loading = false));
    },
    getAudio() {
      axios
          .get("https://api.quran.com/api/v4/chapter_recitations/2/" + this.cari)
          .then((response) => {
            this.audio = response.data.audio_file;
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
  <div class="x text-center">
    <br />
    <br />
    <br />
    <br />
    <h1 class="p">AL- QUR'AN</h1>
    <br />
    <img src="../assets/quranlogo.png" alt="logo" width="400px" />
    <br />
    <br />
    <a type="button" class="pa btn btn-dark border-0" href="#1"
    >Search</a
    >
  </div>
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <div id="1">
    <div class="text-center">
      <h1 class="p">Ketikkan nomor surat yang dicari!</h1>
    </div>
    <div class="search">
      <input
          v-model="cari"
          class="form-control me-2"
          type="search"
          placeholder="Cari Surah (contoh: 114)"
          aria-label="Search"
      />
    </div>

    <div class="text-end" v-if="cari != null">
      <div class="mt-5">
        <h1 class="po text-center">{{ judul.name_complex }}</h1>
        <br />
        <h3 class="p text-center">{{ name.name }}</h3>
        <br />
        <h4 class="p fst-italic text-center">
          {{ "Diturunkan di " + judul.revelation_place }}
        </h4>
      </div>
      <div v-for="(ayat, index) in surah" :key="index" class="card">
        <div class="card-body">
          <h5 class="card-title">{{ index + 1 }}{{ ayat.text_uthmani }}</h5>
          <p class="card-text text-start">Artinya :</p>
          <p v-html="translation[index].text" class="text-start"></p>
        </div>
      </div>
      <br />
      <div class="text-center">
        <div v-if="audio" class="mt-5">
          <h1 class="text-center">{{ "Audio Surah " + judul.name_complex }}</h1>
          <audio v-bind:src="audio.audio_url" controls class="w"></audio>
        </div>
      </div>
    </div>
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
  </div>
</template>
<style scoped>
.p {
  font-family: Roboto;
}
.po {
  font-family: Roboto;
  font-size: 75px;
}
.search {
  width: 400px;
  height: 50px;
  margin-left: 559px;
  margin-top: 15px;
  alignment: center;
}
.pa {
  font-family: Roboto;
  background: linear-gradient(50deg, #032645, #5e5e9d);
  animation: hue-rotate 5s linear infinite alternate;
  border-color: white;
  width: 200px;
  margin-top: 50px;
}
@keyframes hue-rotate {
  to {
    filter: hue-rotate(90deg);
  }
}
.w {
  margin-top: 100px;
}
</style>
