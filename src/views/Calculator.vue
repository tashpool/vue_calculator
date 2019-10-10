<template>
  <v-container>
    <v-row no-gutters justify="center">
      <v-col cols="12">
        <div class="__display rounded_div display-2">0</div>
      </v-col>
    </v-row>

    <v-row no-gutters justify="center">
      <v-col
          v-for="n in ops"
          :key="n"
          cols="12"
          lg="3"
      >
        <v-btn block x-large tile color="primary" class="mx-auto title lighten-2">{{ n }}</v-btn>
      </v-col>
    </v-row>

    <v-row no-gutters>
      <v-col cols="9">
        <v-row no-gutters>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">1</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">2</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">3</v-btn>
          </v-col>
        </v-row>

        <v-row no-gutters justify="center">
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">4</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">5</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">6</v-btn>
          </v-col>
        </v-row>

        <v-row no-gutters justify="center">
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">7</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">8</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">9</v-btn>
          </v-col>
        </v-row>

        <v-row no-gutters justify="center">
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">0</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">.</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">AC</v-btn>
          </v-col>
        </v-row>
      </v-col>

      <v-col cols="3">
        <v-row no-gutters>
          <v-col cols="12">
            <v-btn block height="208" width="100" class="display-1">=</v-btn>
          </v-col>
        </v-row>
      </v-col>

    </v-row>

  </v-container>
</template>

<script>
  export default {
    name: "Calculator",
    data() {
      return {
        ops: ['+', '-', 'x', '÷']
      }
    }
  }
</script>

<style scoped>
.container {
  max-width: 650px;
}
.__display {
  background-color: #222222;
  color: #fff;
  font-size: 1.714285714em;
  padding: 0.5em 0.75em;
  text-align: right;
}

.rounded_div{
  border-radius: 25px 25px 0px 0px;
}
</style>