<template>
  <div id="app">
    <b-navbar toggleable="lg" type="light" variant="light" class="mb-4">
      <b-navbar-brand href="#">Task Management App</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item to="/login">Login</b-nav-item>
          <b-nav-item to="/dashboard">Dashboard</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <div class="container">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
}
</script>

<style>
#app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.navbar {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.container {
  max-width: 1200px;
}

h2 {
  color: #3498db;
  margin-bottom: 1.5rem;
}

.btn-primary {
  background-color: #3498db;
  border-color: #3498db;
}

.btn-primary:hover {
  background-color: #2980b9;
  border-color: #2980b9;
}

.btn-secondary {
  background-color: #95a5a6;
  border-color: #95a5a6;
}

.btn-secondary:hover {
  background-color: #7f8c8d;
  border-color: #7f8c8d;
}
</style>