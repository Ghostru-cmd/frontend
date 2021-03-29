<template>
    <table>
        <thead>
            <tr>
                <th>Название</th>
                <th>Статус</th>
                <th>Отвецтвенный</th>
                <th>Дата создания</th>
                <th>Бюджет</th>
            </tr>
        </thead>
        <tbody>
            <Row 
                v-for="(lead, i) of leads"
                v-bind:lead="lead"
                v-bind:i="i"
            />
        </tbody>
    </table>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Row from './row.vue'

@Component({
    components: {
        Row
    }
})

export default class Table extends Vue {
    leads!: Promise<Array<any>>

    data() {
        return {
            leads: []
        }
    }

    async mounted() {
        this.leads = await fetch('http://localhost:3000/leads').then(response => response.json())
    }   
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