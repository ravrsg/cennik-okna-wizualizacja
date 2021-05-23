<template>
  <v-container>
    <v-col :style="myStyle" cols="12" class="responsive-height bordered centered-bottom">
      <div :style="imgStyle" class="img-style"></div>
    </v-col>
  </v-container>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  data() {
    return {
      myStyle: {
        backgroundColor: null,
        display: "flex",
        alignItems: "flex-end",
        justifyContent: "center",
      },
      imgStyle: {
        width: null,
        height: null,
      },
    };
  },
  created() {
    eventBus.$on("dataSet", (data) => {
      this.myStyle.backgroundColor = data.hex;
      this.imgStyle.height = data.height;
      this.imgStyle.width = data.width;
    });
  },
};
</script>

<style scoped>
.bordered {
  border: 1px solid black;
}
.centered-bottom {
  display: flex;
  align-items: flex-end;
  justify-content: center;
}
.img-style {
  border: 2px solid black;
  background-image: url("../assets/pexels-photo-3573351.png");
}
@media (max-width: 960px) {
  .responsive-height {
    height: 25vh;
  }
}
@media (min-width: 961px) {
  .responsive-height {
    height: 75vh;
  }
}
</style>
