<template>
  <v-container>
    <v-parallax src="https://www.omegawatches.com/images/Watches/Product_Presentation/Seamaster/Seamaster300_Spectre/SE_Seamaster300_Spectre_ambiance1_1600x900.jpg" height="300">
      <v-layout column align-center justify-center>
        <h1 class="white--text">Omega archive</h1>
        <h4 class="white--text">Find your watch</h4>
      </v-layout>
    </v-parallax>
    <v-layout>
      <v-flex xs12 class="text-xs-center">
        <v-progress-circular
          indeterminate
          class="primary--text"
          :width="7"
          :size="70"
          v-if="loading"></v-progress-circular>
      </v-flex>
    </v-layout>
    <v-layout row wrap class="mt-2" v-if="!loading">
      <v-flex xs-12>
        <v-carousel style="cursor: pointer">
          <v-carousel-item
            v-for="meetup in meetups"
            :src="meetup.imageUrl"
            :key="meetup.id"
          @click="onLoadMeetup(meetup.id)">
            <div class="title">
              {{meetup.title}}
            </div>
          </v-carousel-item>
        </v-carousel>
      </v-flex>
    </v-layout>
    <v-layout row wrap class="mt-2">
      <v-flex xs12 class="text-xs-center">
        <ais-index
          app-id="latency"
          api-key="3d9875e51fbd20c7754e65422f7ce5e1"
          index-name="bestbuy"
        >
          <ais-search-box></ais-search-box>
          <ais-results>
            <template scope="{ result }">
              <h2>
                <ais-highlight :result="result" attribute-name="name"></ais-highlight>
              </h2>
            </template>
          </ais-results>
        </ais-index>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    computed: {
      meetups () {
        return this.$store.getters.featuredMeetups
      },
      loading () {
        return this.$store.getters.loading
      }
    },
    methods: {
      onLoadMeetup (id) {
        this.$router.push('/meetups/' + id)
      }
    }
  }
</script>

<style scoped>

  .container {
    max-width:1500px;
    padding: 0px;
  }
  .title {
    position: absolute;
    bottom: 50px;
    background-color: rgba(0,0,0,0.5);
    color:#fff;
    font-size: 2em;
    padding: 20px;
  }

</style>
