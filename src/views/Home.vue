<template>
  <div class="home">
      <Header />
      <Table
        v-bind:leads="leads"
        v-bind:statuses="statuses"
        v-bind:users="users"
      />
      <div class="footer"></div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Header from "../components/header.vue";
import Table from "../components/table.vue";

@Component({
  components: {
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
    fetch('http://localhost:3000/leads').then(response => response.json()).then(data => {this.leads = data})
    // fetch('http://localhost:3000/pipelines').then(response => response.json()).then(data => {this.statuses = data})
    // fetch('http://localhost:3000/pipelines').then(response => response.json()).then(data => {this.users = data})
    // this.users = await fetch('http://localhost:3000/users').then(response => response.json())
  }
  
}
</script>
