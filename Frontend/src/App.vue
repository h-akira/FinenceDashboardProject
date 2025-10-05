<template>
  <div id="app">
    <!-- Bootstrap Navbar -->
    <nav class="navbar navbar-expand-lg bg-dark" data-bs-theme="dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="/">FinanceDashboard</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <!-- <ul class="navbar-nav me-auto"> -->
          <!--   <li class="nav-item"> -->
          <!--     <a class="nav-link active" aria-current="page" href="#">Home</a> -->
          <!--   </li> -->
          <!--   <li class="nav-item"> -->
          <!--     <a class="nav-link" href="#">Features</a> -->
          <!--   </li> -->
          <!--   <li class="nav-item"> -->
          <!--     <a class="nav-link" href="#">Pricing</a> -->
          <!--   </li> -->
          <!-- </ul> -->
          <div class="ms-auto d-flex align-items-center">
            <a href="#" class="btn btn-outline-light me-2">Profile</a>
            <a href="#" class="btn btn-outline-light">Logout</a>
          </div>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <Home />
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>
