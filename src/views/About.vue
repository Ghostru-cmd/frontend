<template>
  <div class="about">
    <Header />
    <TableContacts />
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
  
}
</script>
