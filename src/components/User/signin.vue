<template>
  <v-container>
     <v-layout row v-if="error">
       <v-flex xs12 sm6 offset-sm3>
          <appAlert class="mt-5" @dismissed="onDismissed" :text="error.message"></appAlert>
        </v-flex>
      </v-layout>
      <v-layout row>
          <v-flex xs12 sm6 offset-sm3>
              <v-card class="mb-5">
                  <v-card-text>
                      <v-container>
                          <form @submit.prevent="onSignin">
                            <v-layout row>
                                <v-flex xs12>
                                    <v-text-field
                                    name="email"
                                    label="Mail"
                                    id="email"
                                    v-model="email"
                                    type="email"
                                    prepend-icon="email"
                                    required
                                    ></v-text-field>
                                </v-flex>
                            </v-layout>
                            <v-layout row>
                                <v-flex xs12>
                                    <v-text-field
                                    name="password"
                                    label="Password"
                                    id="password"
                                    v-model="password"
                                    type="password"
                                    required
                                    hint="At least 8 characters"
                                    min="8"
                                    :append-icon="visibility ? 'visibility' : 'visibility_off'"
                                    :append-icon-cb="() => (visibility = !visibility)"
                                    :type="visibility ? 'text' : 'Password'"
                                    prepend-icon="lock"
                                    ></v-text-field>
                                </v-flex>
                            </v-layout>

                            <v-container fluid>
                                <v-layout row wrap>
                                    <v-flex class="mb-4">
                                        <div style="text-align:start">
                                            <div class="mb-2"><a href="#">Forgot Password?</a></div>
                                            <div><a href="./signup">Don't have an Account yet?<br>Create one Now</a></div>
                                        </div>
                                    </v-flex>

                                    <v-spacer></v-spacer>
                                    <v-flex>
                                        <v-btn class="mb-3" success block type="Submit" :disabled="loading" :loading="loading">
                                          Login Now
                                          <span slot="loader" class="custom-loader">
                                            <v-icon light>cached</v-icon>
                                          </span>
                                        </v-btn>
                                        <hr></hr>
                                        <v-btn class="mt-3" error block dark  @click.native="signUserWithGoogleAuth()">
                                          <v-icon fa class="v-icon">google</v-icon>
                                          Login With Google
                                        </v-btn>
                                        <v-btn primary block dark @click.native="signUserWithFacebookAuth()">
                                          <v-icon fa class="v-icon">facebook</v-icon>
                                          Login With Facebook
                                        </v-btn>
                                    </v-flex>                              
                                </v-layout>
                            </v-container>

                          </form>
                          
                      </v-container>
                  </v-card-text>
              </v-card>
          </v-flex>
      </v-layout>
   </v-container>
</template>

<script>
export default {
  data () {
    return {
      email: '',
      password: '',
      visibility: false
    }
  },
  computed: {
    user () {
      return this.$store.getters.user
    },
    error () {
      return this.$store.getters.error
    },
    loading () {
      return this.$store.getters.loading
    }
  },
  watch: {
    user (value) {
      if (value !== null && value !== undefined) {
        this.$router.push('/')
      }
    }
  },
  methods: {
    onSignin () {
      this.$store.dispatch('signUserIn', {email: this.email, password: this.password})
    },
    onDismissed () {
      this.$store.dispatch('clearError')
    },
    signUserWithGoogleAuth () {
      this.$store.dispatch('signUserWithGoogleAuth')
    },
    signUserWithFacebookAuth () {
      this.$store.dispatch('signUserWithFacebookAuth')
    }
  }
}
</script>

<style scoped>

</style>
