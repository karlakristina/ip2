<template>
<div>
      <v-autocomplete
      v-model="drzava"
      :items="rijeci"
      dense
      filled
      @input="dohvatisv();prikazsnackbara();dohvatslike()"
    ></v-autocomplete>


    <div class="text-center ma-2">
    <v-btn
      dark
      color="green"
      v-show="prikazi"
      v-bottom="dolje"
    >
      Uspješno dohvaćeno!
    </v-btn>
    <v-snackbar
      v-model="snackbar"
    >
      {{ text }}

      <template v-slot:action="{ attrs }">
        <v-btn
          color="red"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Nešto je pošlo po krivu!
        </v-btn>
      </template>
    </v-snackbar>
  </div>
    <v-row>
      <v-col cols="4" v-for="sveuciliste in sveucilista" :key="sveuciliste.name">

    <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img height="230"
      :src="dohvatslike(sveuciliste.web_pages[0])"
    ></v-img>

    <v-card-title> {{sveuciliste.name}} </v-card-title>

    <v-card-text>
      <v-row
        align="center"
        class="mx-0"
      >
        <v-rating
          :value="4.5"
          color="amber"
          dense
          half-increments
          readonly
          size="14"
        ></v-rating>

        <div class="grey--text ms-4">
          4.5 (413)
        </div>
      </v-row>

      <div class="my-4 text-subtitle-1">
        $ • Italian, Cafe
      </div>

      <div>Small plates, salads & sandwiches - an intimate setting with 12 indoor seats plus patio seating.</div>
    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-title>Tonight's availability</v-card-title>

    <v-card-text>
      <v-chip-group
        v-model="selection"
        active-class="deep-purple accent-4 white--text"
        column
      >
        <v-chip>5:30PM</v-chip>

        <v-chip>7:30PM</v-chip>

        <v-chip>8:00PM</v-chip>

        <v-chip>9:00PM</v-chip>
      </v-chip-group>
    </v-card-text>

    <v-card-actions>
      <v-btn
        color="deep-purple lighten-2"
        text
        @click="reserve"
      >
        Reserve
      </v-btn>
    </v-card-actions>
  </v-card>
  </v-col>
</v-row>

</div>

  
</template>

<script>
  

  export default {
    name: 'Home',
    data () {
      return {
        rijeci: ["croatia", "spain", "italy"],
        drzava: null,
        sveucilista: [],
        dialog: false,
        text: "Snackbar!",
        prikazi: false,
        dolje: false,
      }
    }, 
    methods: {
      dohvatisv: function() {
        this.axios
        .get("http://universities.hipolabs.com/search?country=" + this.drzava)
        .then((response) => {
          console.log(response.data);
          this.sveucilista = response.data;
        });
    },
    created (){
      this.dohvatisv();

    },
    dohvatslike: function (slika) {
      return (
        "https://api.microlink.io/?screenshot&embed=screenshot.url&url=" + slika
      );
    },
    prikazsnackbara(){
      this.prikazi=true;
      this.dolje=true;
      },



      }
    }

</script>
