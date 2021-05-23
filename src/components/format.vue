<template>
  <v-container>
    <v-row>
      <v-col cols="9">
        <v-text-field label="Cena za 1m2" prefix="PLN" type="number" v-model="unitPrice"></v-text-field
      ></v-col>
      <v-col cols="3" class="centered"
        ><v-btn @click="reset()">
          Reset
        </v-btn></v-col
      >
    </v-row>
    <v-row>
      <v-col cols="10">
        <v-slider label="Szerokość:" max="900" min="0" v-model="width"></v-slider>
      </v-col>
      <v-col cols="2"> {{ width }} cm</v-col>
    </v-row>
    <v-row>
      <v-col cols="10">
        <v-slider label="Wysokość:" max="200" min="0" v-model="height"></v-slider>
      </v-col>
      <v-col cols="2"> {{ height }} cm</v-col>
    </v-row>
    <p>Kolor ściany</p>
    <v-btn-toggle v-model="myStyle.backgroundColor" tile color="grey darken-2 accent-3" group>
      <v-btn value="#FF0000">
        Czerwony
      </v-btn>
      <v-btn value="#00FF00">
        Zielony
      </v-btn>
      <v-btn value="#FFFF00">
        Żółty
      </v-btn>
    </v-btn-toggle>

    <v-text-field label="HEX" v-model="myStyle.backgroundColor"></v-text-field>
    <v-alert dense outlined type="error" v-if="alert.length > 0">
      {{ alert }}
    </v-alert>

    <v-card>
      <v-card-title>
        Cena:
      </v-card-title>
      <v-card-title primary> {{ price }} </v-card-title>
    </v-card>
  </v-container>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  computed: {
    price() {
      let p;
      if (
        this.width === null ||
        this.height === null ||
        this.unitPrice === null ||
        this.alert.length > 0 ||
        this.myStyle.backgroundColor === null
      ) {
        p = "Podaj wszystkie parametry.";
      } else {
        p = ((this.width / 100) * (this.height / 100) * this.unitPrice).toFixed(2) + "zł";
      }
      return p;
    },
  },
  data() {
    return {
      width: null,
      height: null,
      unitPrice: null,
      myStyle: {
        backgroundColor: "#FFFFFF",
      },
      alert: "",
    };
  },
  watch: {
    "myStyle.backgroundColor": {
      handler: function() {
        if (!/^#(?:[0-9a-fA-F]{3}){1,2}$/.test(this.myStyle.backgroundColor)) {
          this.alert = "Niepoprawny format koloru HEX.";
        } else {
          this.alert = "";
          this.emit();
        }
      },
      deep: true,
    },
    price() {
      this.emit();
    },
    width() {
      this.emit();
    },
    height() {
      this.emit();
    },
    unitPrice() {
      this.emit();
    },
  },
  methods: {
    emit() {
      eventBus.$emit("dataSet", {
        hex: this.myStyle.backgroundColor,
        width: (this.width * 100) / 900 + "%",
        height: (this.height * 100) / 200 + "%",
      });
    },
    reset() {
      this.width = null;
      this.height = null;
      this.unitPrice = null;
      this.alert = "";
      this.myStyle.backgroundColor = "#FFFFFF";
    },
  },
};
</script>

<style scoped>
.centered {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
