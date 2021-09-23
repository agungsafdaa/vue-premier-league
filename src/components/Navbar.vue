<template>
 
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#"><img class="img-logo" src="../assets/images/logo.png"/></b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/foods">Foods</router-link>
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
           
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  
</template>

<script>

export default {
  name: "Navbar",

};
</script>

<style></style>
© 2021 GitHub, Inc.