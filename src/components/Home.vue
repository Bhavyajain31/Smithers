<template>
<div class="home">
  <!-- Navbar -->
  <v-toolbar flat color="indigo darken-1">
    <router-link to="/">
    <v-toolbar-title style="color: white; font-size: 30px; font-family: Product Sans;">Smithers</v-toolbar-title>
    </router-link>
  </v-toolbar>
  <!-- Welcome -->
  <v-container grid-list-md text-xs-center style="margin-top: 10%;">
    <v-layout row wrap>
      <v-flex md6 xs12>
        <div>
          <h1 class="font-weight-regular" style="color: white; font-size: 45px;">Welcome to Smithers.</h1>
          <h3 class="font-weight-regular" style="color: white; font-size: 18px;">Your assistant for creating business cards</h3>
          <br>
          <v-text-field
            label="Solo"
            id="fullname"
            placeholder="What's your fullname?"
            solo
            flat
            v-model="fullname"
          ></v-text-field>
          <br>
          <v-btn v-on:click="card" round depressed color="indigo darken-1"><div style="color: white;">Make a business card</div></v-btn>
        </div>
      </v-flex>
      <v-flex md6 class="hidden-sm-and-down">
        <div>
          <img src="static/smithers.jpg" alt="" height="400" width="400">
        </div>
      </v-flex>
    </v-layout>
  </v-container>
  <!-- footer -->
<v-footer
    height="20"
    color="indigo darken-1"
    app
  >
    <v-layout
      justify-center
      row
      wrap
    >
      <v-btn color="white" href="https://github.com/Merwanedr/smithers" title="source code" flat small icon><div style="color: white; font-size: 20px;"><i class="fab fa-github"></i></div></v-btn> <!-- add github link -->
      <v-btn href="https://merwanedr.github.io/" color="transparent" flat small round><div style="color: white;"><i class="fas fa-heart"></i> Support </div></v-btn>
      <v-btn color="transparent" flat small round><div style="color: white;">© 2018 Merwane Draï</div></v-btn>
    </v-layout>
  </v-footer>
</div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      fullname: ''
    }
  },
  created() {

  },
  methods: {
    async card() {
      if (this.fullname === '') {
        document.getElementById('fullname').placeholder = "Please enter your fullname...";
        document.getElementById('fullname').style.borderBottom = "2px solid rgba(183,28,28,0.3)";
      }
      if (this.fullname !== '') {
        sessionStorage.setItem("fullname", this.fullname);
        this.$router.push({
          name: 'Card'
        })
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
