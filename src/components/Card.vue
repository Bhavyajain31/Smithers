<template>
<div class="card">
<!-- Navbar -->
  <v-toolbar flat color="indigo darken-1" fixed>
    <router-link to="/">
    <v-toolbar-title style="color: white; font-size: 30px; font-family: Product Sans;">Smithers</v-toolbar-title>
    </router-link>
    <v-spacer></v-spacer>
    <div style="color: white; font-size: 17px;">{{ fullname }}</div>
  </v-toolbar>
  <!-- Main -->
  <div class="mainPage">
  <v-container>
    <v-layout row wrap>
      <v-flex md5 xs12 style="margin-top: 25px;">
        <!-- email -->
        <v-text-field
            label="Solo"
            type="email"
            id="email"
            placeholder="Enter your email"
            solo
            flat
            v-model="email"
          ></v-text-field>
          <!-- Phone number -->
          <v-text-field
            label="Solo"
            type="phone"
            id="phone"
            placeholder="Enter your phone number"
            solo
            flat
            v-model="phoneNumber"
          ></v-text-field>
          <!-- location -->
          <v-text-field
            label="Solo"
            type="text"
            id="location"
            placeholder="Enter your location"
            solo
            flat
            v-model="location"
          ></v-text-field>
          <!-- portfolio -->
          <v-text-field
            label="Solo"
            type="text"
            id="portfolio"
            placeholder="Enter your LinkedIn or your portfolio link"
            solo
            flat
            v-model="portfolio"
          ></v-text-field>
          <!-- job -->
          <v-text-field
            label="Solo"
            type="text"
            id="job"
            placeholder="What's your job?"
            solo
            flat
            v-model="job"
          ></v-text-field>
          <div style="text-align: center; color: white; font-size: 15px;">Color Picker: </div>
          <br>
          <v-layout row>
            <!-- Primary Color Picker -->
            <v-flex xs5 style="text-align: center;">
              <div style="color: white; font-size: 15px;">Primary Color</div>
              <input type="color" v-model="primaryColor" value="#00000" class="colorPicker">
            </v-flex>
            <v-flex xs2>
              <!-- Empty -->
            </v-flex>
            <!-- Secondary Color Picker -->
            <v-flex xs5 style="text-align: center;">
              <div style="color: white; font-size: 15px;">Secondary Color</div>
              <input type="color" v-model="secondaryColor" value="#9E9E9E" class="colorPicker">
            </v-flex>
          </v-layout>
          <!-- Generate -->
          <div style="text-align: center; margin-top: 20px;">
            <v-btn v-on:click="savecard" depressed round color="indigo darken-1"><div style="color: white">Create</div></v-btn>
          </div>
      </v-flex>
      <v-flex md2 xs12>
        <!-- empty -->
      </v-flex>
      <v-flex md5 xs12 style="margin-top: 25px;" class="hidden-sm-and-down">
        <!-- Card Preview -->
        <h1 style="color: white;">Preview: </h1>
      <!-- Recto -->
      <div id="recto-card" class="cardPreview" :style="{'border-color': secondaryColor}">
        <div class="fullnameCard font-weight-light" :style="{'color': primaryColor}">{{fullname}}</div>
        <div class="jobCard" :style="{'color': secondaryColor}">{{job.toUpperCase()}}</div>
        <br>
        <br>
        <div class="locationCard" :style="{'color': secondaryColor}"><i class="fas fa-map-marker-alt"></i> {{location}}</div>
      </div>
      <br>
      <br>
      <!-- Verso -->
      <div id="verso-card" class="cardPreview" :style="{'border-color': secondaryColor}">
        <v-layout row>
          <v-flex xs6 style="padding-bottom: 100px;" :style="{'background-color': secondaryColor}">
        <br>
        <br>
        <br>
        <br>
        <div class="labelCard" style="color: white;"><strong>Email: </strong></div>
      <div class="infoCard" :style="{'color': primaryColor}">{{email}}</div>
        <br>
        <br>
        <div class="labelCard" style="color: white;"><strong>Phone: </strong></div>
      <div class="infoCard" :style="{'color': primaryColor}">{{phoneNumber}}</div>
          </v-flex>
          <v-flex xs6 style="text-align: center;">
            <br>
            <br>
            <br>
          <div class="portfolioCard" :style="{'color': primaryColor}"><strong>{{portfolio}}</strong></div>
          </v-flex>
        </v-layout>
      </div>
      <br>
      <br>
      </v-flex>
    </v-layout>
  </v-container>
</div>
<br>
<br>
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
      <v-btn color="white" href="https://github.com/Merwanedr/smithers" title="source code" flat small icon><div style="color: white; font-size: 20px;"><i class="fab fa-github"></i></div></v-btn> 
      <v-btn href="https://merwanedr.github.io/" color="transparent" flat small round><div style="color: white;"><i class="fas fa-heart"></i> Support </div></v-btn>
      <v-btn color="transparent" flat small round><div style="color: white;">© 2018 Merwane Draï</div></v-btn>
    </v-layout>
  </v-footer>
</div>
</template>

<script>
import domtoimage from 'dom-to-image';
import saveAs from 'file-saver';
export default {
  name: 'Card',
  data () {
    return {
      fullname: sessionStorage.getItem('fullname'),
      email: '',
      phoneNumber: '',
      location: '',
      portfolio: '',
      job: '',
      primaryColor: '',
      secondaryColor: ''
    }
  },
  beforeCreate() {
    if (sessionStorage.getItem('fullname') === null) {
      this.$router.push({
          name: 'Home'
        })
    }
  },
  created() {
    
  },
  methods: {
    savecard() {
      // recto
      domtoimage.toBlob(document.getElementById('recto-card'))
    .then(function (blob) {
        window.saveAs(blob, 'card-recto.png');
    });
      // verso
    domtoimage.toBlob(document.getElementById('verso-card'))
    .then(function (blob) {
        window.saveAs(blob, 'card-verso.png');
    });
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mainPage{
  margin-top: 80px;
}
.colorPicker{
  width: 120px;
  height: 40px;
  color: white;
}
.cardPreview{
  border: 4px solid; /* Secondary color*/
  background-color: white;
  height: 300px;
  width: 525px;
}
.fullnameCard{
  font-size: 40px;
  padding-top: 90px;
  text-align: center;
  color: black; /* Primary color*/
}
.jobCard{
  text-align: center;
  font-size: 18px;
  letter-spacing: 3px;
  padding-top: 10px;
  color: black; /* Secondary color*/
}
.locationCard{
  text-align: center;
  font-size: 18px;
  letter-spacing: 1px;
  color: grey; /* Secondary color*/
}
.infoCard{
  text-align: center;
  font-size: 15px;
  color: black; /* Primary color*/
}
.labelCard{
  text-align: center;
  font-size: 15px;
  color: gray; /* Secondary color*/
}
.portfolioCard{
  padding-top: 70px;
}
</style>
