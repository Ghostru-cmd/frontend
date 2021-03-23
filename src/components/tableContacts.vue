<template>
    <table>
        <thead>
            <tr>
                <th>Имя</th>
                <th>Телефон</th>
                <th>Email</th>
            </tr>
        </thead>
        <tbody>
            <RowContact 
                v-for="(contact, i) of contacts"
                v-bind:contact="contact"
                v-bind:i="i"
            />
        </tbody>
    </table>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import RowContact from './rowContact.vue'

@Component({
  components: {
    RowContact
  },
  props: {
        contacts: Array
    }
})
export default class TableContacts extends Vue {
}
</script>

<style scoped>
table{
    margin-left: 50px;
    margin-right: 50px;
    border-collapse: collapse;
}
thead{
    background: #fafafa;
    font-size: 16px;
}
tbody{
    background-color: white;
    font-size: 14px;
}
th{
    width: 400px;
    height: 50px;
}
</style>