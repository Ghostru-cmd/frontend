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
                v-bind:statuses="statuses"
                v-bind:users="users"
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
    },
    props: ['leads', 'statuses', 'users']
})

export default class Table extends Vue {
    
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