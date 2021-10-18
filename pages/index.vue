<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">Nuxt Firebase v9</h1>
      <div class="links">
        <button class="button--green shadow" @click="register">Register</button>
        <button class="button--green shadow" @click="login">Login</button>
        <button class="button--green shadow" @click="logout">Logout</button>
        <button class="button--green shadow" @click="getUser">
          Current User
        </button>
        <button class="button--green shadow" @click="clearScreen">
          Clear Screen
        </button>
        <button class="button--green shadow" @click="sendMailVerification">
          Verify Email
        </button>
        <button class="button--red shadow" @click="deleteUser">
          Delete User
        </button>
      </div>
      <div class="align-left">
        Current user :
        <pre>{{ currentUser }}</pre>
        Error:
        <pre>{{ response }}</pre>
      </div>
      <div>Demo Firebase v9</div>
      <br />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      response: '',
      currentUser: {},
      email: 'demo_firebase@mailinator.com',
      password: '123456',
    }
  },
  computed: {},
  mounted() {
    this.$fire.auth.onAuthStateChanged((u) => {
      console.log('auth user changed ', u)
    })
  },
  methods: {
    async register() {
      try {
        this.clearResponse()
        const response = await this.$fire.createUserWithEmailAndPassword(
          this.$fire.auth,
          this.email,
          this.password
        )
        // this.response = response
        console.log({ response })
        this.getUser()
      } catch (error) {
        this.response = { errorCode: error.code, errorMessage: error.message }
      }
    },
    async login() {
      try {
        this.clearResponse()
        const response = await this.$fire.signInWithEmailAndPassword(
          this.$fire.auth,
          this.email,
          this.password
        )
        // this.response = response
        console.log({ response })
        this.getUser()
      } catch (error) {
        this.response = { errorCode: error.code, errorMessage: error.message }
      }
    },
    async logout() {
      try {
        this.clearResponse()
        const response = await this.$fire.signOut(this.$fire.auth)
        // this.response = response
        console.log({ response })
        this.getUser()
      } catch (error) {
        this.response = { errorCode: error.code, errorMessage: error.message }
      }
    },
    clearResponse() {
      this.response = {}
    },
    clearScreen() {
      this.currentUser = {}
      this.clearResponse()
    },
    getUser() {
      if (!this.$fire.auth.currentUser) {
        this.currentUser = Object.assign({}, {})
        return
      }

      const { displayName, email, emailVerified } = this.$fire.auth.currentUser

      this.currentUser = Object.assign(
        {},
        { displayName, email, emailVerified }
      )
    },
    async sendMailVerification() {
      try {
        this.clearResponse()
        const response = await this.$fire.sendEmailVerification(
          this.$fire.auth.currentUser
        )
        // this.response = response
        console.log({ response })
        this.getUser() // TODO: how update this status verified
      } catch (error) {
        this.response = { errorCode: error.code, errorMessage: error.message }
      }
    },
    async deleteUser() {
      try {
        this.clearResponse()
        const response = await this.$fire.deleteUser(
          this.$fire.auth.currentUser
        )
        // this.response = response
        console.log({ response })
        this.getUser() // TODO: how update this status verified
      } catch (error) {
        this.response = { errorCode: error.code, errorMessage: error.message }
      }
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.align-left {
  align-items: left;
  text-align: left;
}
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
