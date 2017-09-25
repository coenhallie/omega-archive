<template>
  <v-container fluid grid-list-sm>
    <v-layout row wrap v-for="meetup in meetups" :key="meetup.id" class="mb-2">
      <v-flex xs3>
        <v-card class="info" tile flat>
          <v-container fluid grid-list-lg>
            <v-layout row wrap>
              <v-flex>
                <v-card-media
                  :src="meetup.imageUrl"
                  height="130px"
                ></v-card-media>
                <v-card-title primary-title>
                  <div>
                    <h5 class="white--text mb-0">{{meetup.title}}</h5>
                    <div>{{meetup.date | date}}</div>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-btn flat :to="'/meetups/' + meetup.id">
                    <v-icon left light>arrow_forward</v-icon>
                    View meetup
                  </v-btn>
                </v-card-actions>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    computed: {
      meetups () {
        return this.$store.getters.loadedMeetups
      }
    }
  }

</script>

<style>

</style>
