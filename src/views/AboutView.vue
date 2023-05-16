<script>
import NavBar from "../components/NavBar.vue";
export default {
  name: "AboutView",
  components: { NavBar},
};
</script>

<template>
  <NavBar />
  <!-- About-->
  <br />
  <br />
  <br />
  <br />
  <br />
  <section id="about">
    <div class="mt-5">
      <h1>About Us</h1>
      <p>
        Al-Quran was founded in 2023. The website aims to make it easy for anyone to read, study, and learn the Quran.
      </p>
    </div>
    <div class="my-5">
      <h1>Credits</h1>
      <p>
        First of All,by the grace of Allah,I have become able to create this website to make Al-Qur'an available to all the people in online. Actually,I used An API which is developed by some great developers and i also take the idea of FrontEnd of this website from Quran.com . Thanks to Quran.com's developers to give us a great API and cool Quran website.
      </p>
    </div>
    <div class="container">
      <div class="row text-center mt-5">
        <div class="col">
        </div>
      </div>
    </div>
  </section>
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
  <!-- Akhir About-->

  <!-- Table -->
  <section class="container my-5">
    <div class="row justify-content-center">
      <div class="col-8">
        <div class="card rounded shadow">
          <div class="card-header">About Me</div>
          <div class="card-body text-start">
            <table class="table">
              <tbody>
              <tr>
                <td>Name</td>
                <td>:</td>
                <td>Widya Maulida Putri</td>
              </tr>
              <tr>
                <td>University</td>
                <td>:</td>
                <td>UIN Sultan Syarif Kasim Riau</td>
              </tr>
              <tr>
                <td>Major</td>
                <td>:</td>
                <td>Teknik Informatika</td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!-- Akhir Table -->
</template>

<style scoped></style>
