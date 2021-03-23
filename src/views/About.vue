<template>
  <div class="about">
    <Header />
    <TableContacts
      v-bind:contacts="contacts"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Header from "../components/header.vue";
import TableContacts from "../components/tableContacts.vue";

@Component({
  components: {
    Header,
    TableContacts
  }
})

export default class About extends Vue {
  contacts!: Promise<any>

  data() {
    return {
      contacts: []
    }
  }
  async mounted(){
    this.contacts = await fetch('http://localhost:3000/contacts').then(response => response.json())
  }
}
</script>
