<template>
  <div class="login">
    <h2 class="mb-4">Login</h2>
    <form @submit.prevent="login">
      <div class="mb-3">
        <label for="email" class="form-label">Email:</label>
        <input type="email" id="email" v-model="email" class="form-control" required>
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Password:</label>
        <input type="password" id="password" v-model="password" class="form-control" required>
      </div>
      <button type="submit" class="btn btn-primary">Login</button>
    </form>
    <p class="mt-3">
      Don't have an account? 
      <router-link to="/register">Register here</router-link>
    </p>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    login() {
      // Implement login logic here
      console.log('Login attempt:', this.email, this.password)
      // For demo purposes, we'll just redirect to the dashboard
      this.$router.push('/dashboard')
    },
  },
}
</script>