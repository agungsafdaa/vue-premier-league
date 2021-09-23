<template>
  <div class="home">
    <Navbar />
    <Hero />
    <div class="container">
      <div class="row mt-70">
        <div class="col-md">
          <h4>No Rooms For <strong>Racism</strong></h4>
        </div>
      </div>

      <div class="row mb-3">
        <div
          class="col-md-3 mt-4"
          v-for="standings in standings"
          :key="standings.stage"
        >
          <h6>Klasemen Sementara</h6>
          <div class="card table  mt-3">
            <table class="table table-sm">
              <thead>
                <tr>
                  <th><p>Position</p></th>
                  <th><p>Club</p></th>
               
                  <th><p>Pts</p></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="tables in standings.table" :key="tables.position">
                  <td>{{ tables.position }}</td>
                  <td>
                    <div class="media">
  <img
                      class="mr-3 img-fluid"
                      :src="'' + tables.team.crestUrl"
                      style="width: 15px"
                    />
                    </div>
                  
                   <div class="media-body">
                      <h6>  {{ tables.team.name }}</h6>
                   </div>
                  </td>

                  <td>
                    <strong> {{ tables.points }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        <div class="col-md-9">
          <!-- pertandingan berakhir -->
                     <div class="row mt-70">
            <div class="col-md">
              <h6>Pertandingan <strong>Terakhir</strong></h6>
            </div>
            <div class="col-md">
              <router-link
                to="/foods"
                class="btn btn-md btn-success float-right"
                >Lihat Semua <b-icon-eye></b-icon-eye
              ></router-link>
            </div>
          </div>
          <div class="row mt-10">
            <div
              class="col-md-6 mb-10"
              v-for="matched in finishShowed"
              :key="matched.id"
            >
              <div class="card">
                <p>
                  {{ matched.awayTeam.name }} <span class="matchScore">  {{matched.score.fullTime.awayTeam}}</span> vs  <span class="matchScore">  {{matched.score.fullTime.homeTeam}}</span> {{ matched.homeTeam.name }}
                </p>
                <p>{{ matched.utcDate }}</p>
              </div>
            </div>
          </div>

            <!-- end -->
          <div class="row mt-70">
            <div class="col-md">
              <h6>Pertandingan <strong>Selanjutnya</strong></h6>
            </div>
            <div class="col-md">
              <router-link
                to="/foods"
                class="btn btn-md btn-success float-right"
                >Lihat Semua <b-icon-eye></b-icon-eye
              ></router-link>
            </div>
          </div>
        
          <div class="row mt-10">
            <div
              class="col-md-6 mb-10"
              v-for="matched in matchShowed"
              :key="matched.id"
            >
              <div class="card">
                <p>
                  {{ matched.awayTeam.name }} vs  {{ matched.homeTeam.name }}
                </p>
                <p>{{ matched.utcDate }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src

// var date = new Date();
// date.setDate(date.getDate() + 7);

// console.log(date);
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import Hero from "@/components/Hero.vue";
// import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";
export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    // CardProduct,
    Footer,
  },
  data() {
    return {
      standings: [],
      tables: [],
      team: [],
      matches: [],
      finished: [],
      limit: 6,
      finish:4
    };
  },
  computed: {
    matchShowed() {
      return this.matches.filter((el, index) => index < this.limit);
    },
    finishShowed() {
      return this.finished.filter((el, index) => index < this.finish);
    },
  },
  methods: {
    setProduct(data) {
      this.standings = data;
    },
    setMatches(data) {
      this.matches = data;
    },
    setFinish(data) {
      this.finished = data;
    },
  },

  mounted() {
    const headers = {
      "X-Auth-Token": "9f82aef79b784b6b918beb1865a22581",
    };
    axios
      .get(
        "https://api.football-data.org/v2/competitions/2021/standings?standingType=HOME",
        { headers }
      )
      .then(
        (response) =>
          console.log(response.data.standings) +
          this.setProduct(response.data.standings)
      )
      // handle success
      .catch((error) => console.log(error));
    axios
      .get(
        "https://api.football-data.org/v2/competitions/2021/matches?status=SCHEDULED",
        { headers }
      )
      .then(
        (response) =>
          console.log(response.data) + this.setMatches(response.data.matches)
      )
      // handle success
      .catch((error) => console.log(error));
    axios
      .get(
        "https://api.football-data.org/v2/competitions/2021/matches?status=FINISHED",
        { headers }
      )
      .then(
        (response) =>
          console.log(response.data) + this.setFinish(response.data.matches)
      )
      // handle success
      .catch((error) => console.log(error));
  },
};
</script>
