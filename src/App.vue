  <template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title>Vue Calculator</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
// import Calculator from "@/views/Calculator"

export default {
  name: 'App',
  data: () => ({
    //
  }),
};
</script>
