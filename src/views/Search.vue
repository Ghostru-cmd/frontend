<template>
  <div class="home">
      <Header />
      <Table
        v-cloak
        v-bind:leads="leads"
        v-bind:statuses="statuses"
        v-bind:users="users"
      />
      <div class="footer"></div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
// import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import Header from "../components/header.vue";
import Table from "../components/table.vue";

@Component({
  components: {
    // HelloWorld,
    Header,
    Table
  },
})
export default class Home extends Vue {
  leads!: Promise<any>
  statuses!: Promise<any>
  users!: Promise<any>
  
  data() {
    return {
      leads: [],
      statuses: [],
      users: []
    }
  }

  async mounted(){
    let urlParams = new URLSearchParams(window.location.search);
    let query = urlParams.get('search')
    fetch(`http://localhost:3000/search?${query}`).then(response => response.json()).then(data => {this.leads = data})
    fetch('http://localhost:3000/pipelines').then(response => response.json()).then(data => {this.statuses = data})
    this.users = await fetch('http://localhost:3000/users').then(response => response.json())
  }
  
}
</script>

<style>
[v-cloak] {
  display: none;
}
</style>
