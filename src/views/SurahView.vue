<script>
import { ref } from "vue";
import axios from "axios";
import NavBar from "../components/NavBar.vue";


export default {
  components: { NavBar },
  data(){
    return {
      error: false,
      loading: true,
      info: '',
      surah: ref([]),
      infosurah: ref([])
    }
  },
  mounted() {
    this.getSurah()
    this.getInfoSurah()
  },
  methods: {
    getSurah(){
      axios.get('https://api.quran.com/api/v4/chapters/' + this.$route.params.id)
      .then(response =>
      {
        this.surah = response.data.chapter
      })
      .catch(error =>
      {
      console.log(error)
      this.error = true
      })
      .finally(() => this.loading = false)
    },
    getInfoSurah(){
      axios.get('https://api.quran.com/api/v4/chapters/' + this.$route.params.id + '/info/?language=67')
      .then(response =>
      {
        this.infosurah = response.data.chapter_info
        this.info = this.infosurah.text
      })
      .catch(error =>
      {
        console.log(error)
        this.error = true
      })
      .finally(() => this.loading = false)
    }
  }

}
</script>

<template>
 <NavBar/>
  <div class="text-center">
    <br>
    <br>
    <br>
    <h1>Surah {{ surah.name_complex }}</h1>
    <p v-html="info"></p>
  </div>
</template>
<style scoped>

</style>