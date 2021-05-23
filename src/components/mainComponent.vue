<template>
  <v-container>
    <v-row>
      <v-col cols="12" xl="8" lg="8" md="8" sm="12" xs="12">
        <pic id="printMe"></pic>
        <v-btn @click="print()">Zapisz wizualizację</v-btn>
      </v-col>
      <v-col cols="12" xl="4" lg="4" md="4" sm="12" xs="12">
        <format></format>
      </v-col>
    </v-row>
    <v-dialog v-model="dialog" width="100%">
      <div id="img" />
    </v-dialog>
  </v-container>
</template>

<script>
import format from "./format";
import pic from "./pic";

import html2canvas from "html2canvas";
export default {
  components: {
    format: format,
    pic: pic,
  },
  data() {
    return {
      dialog: false,
    };
  },
  methods: {
    print() {
      html2canvas(document.getElementById("printMe")).then(function(canvas) {
        canvas.toBlob(function(blob) {
          var link = window.URL.createObjectURL(blob);
          window.open(link, "_blank");
        });
      });
    },
  },
};
</script>

<style></style>
