<template>
  <v-container>
    <v-layout row wrap>
      <v-flex xs12 sm10 md8 offset-sm1 offset-md2>
        <v-card class="mb-2 mt-2" v-for="meetup of meetups" :key="meetup.id">
          <v-container fluid>
            <v-layout>
              <v-flex xs5 sm4 md3>
                <v-card-media :src='meetup.imageUrl' height='130px'></v-card-media>
              </v-flex>
              <v-flex sm9 md8>
                <v-card-title primary-title>
                  <div>
                    <h5 class="mb-0">{{ meetup.title }}</h5>
                    <div>{{ meetup.date | date}}</div>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-btn flat :to="'/meetups/'+ meetup.id" class="black--text">
                    <v-icon left light>arrow_forward</v-icon>
                    View Meetup
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
  data () {
    return {
      dialog: false
    }
  },
  computed: {
    meetups () {
      return this.$store.getters.loadedMeetups
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.v-btn{
  margin: 0px;
}

</style>
