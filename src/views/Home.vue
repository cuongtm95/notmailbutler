<template>
  <div class="home">
    <section class="hero is-primary is-fullheight">
      <!-- Login Form --->
      <div v-if="isAuthenticated == false" class="hero-body">
        <div class="container">
          <div class="columns is-centered">
            <div class="column is-5-tablet is-4-desktop is-3-widescreen">
              <form @submit.prevent="login" class="box">
                <div class="field">
                  <label for="" class="label">Email</label>
                  <div class="control">
                    <input type="email" placeholder="user@example.com" class="input" v-model="input.email" required>
                  </div>
                </div>
                <div class="field">
                  <label for="" class="label">Password</label>
                  <div class="control">
                    <input type="password" placeholder="*******" class="input" v-model="input.password" required>
                  </div>
                </div>
                <div class="field">
                  <label for="" class="checkbox">
                    <input type="checkbox">
                  Remember me
                  </label>
                </div>
                <div class="field">
                  <button class="button is-success">
                    Login
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      <!-- Notes -->
      
    </section>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  name: 'home',
  data() {
    return {
      input: {
        email: "",
        password: ""
      },
      isAuthenticated: true,
    }
  },
  methods: {
    login() {
      axios({
        method: 'post',
        url: 'https://beta.mailbutler.io/api/v2/users/login',
        data: {
          email: this.input.email,
          password: this.input.password,
        },
        returnSecureToken:true
      })
      .then(res => {
        this.$router.push(this.$route.query.redirect || '/about')
        console.log(res)
      })
      .catch(error =>console.log(error),
      /* alert('Wrong email or password') */
      )
    }
  }
}
</script>