<template>
    <tr class='row' :id="i">
        <th class='name'>
            {{lead.name}}
            <span class="tags" v-if="lead._embedded.tags != undefined">
                <Tags 
                    v-for="tag of lead._embedded.tags"
                    v-bind:tag="tag"
                />
            </span>
        </th>
        <th class='status' v-if="status != undefined"><span :style="{backgroundColor: status.color}">{{status.name}}</span></th>
        <th class='person'>{{person}}</th>
        <th class='create'>{{create}}</th>
        <th class='prise'>{{prise}}</th>
    </tr>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Tags from './tags.vue'

@Component({
  components: {
    Tags
  },
  props: ['name', 'i', 'lead', 'statuses', 'users']
})
export default class Row extends Vue {
    lead!: any
    statuses!: any
    users!: any
    status!: any
    person!: any
    create!: any
    prise!: any

    data() {
        return {
            status: undefined,
            person: "",
            create: "",
            prise: ""
        }
    }

    created(): void {
        setTimeout(
        (async () => {
            await fetch('http://localhost:3000/pipelines').then(response => response.json())
            
            for (let i: number = 0; i < this.statuses.length && this.status == undefined; i++){
                this.status = this.statuses[i]._embedded.statuses.find((status: any) => status.id == this.lead.status_id)
            }
            
            let pers: any = this.users.find((user: any) => user.id == this.lead.responsible_user_id)
            this.person = shortName(pers.name)
            this.create = getDay(new Date(this.lead.created_at * 1000))
            this.prise = this.lead.price.toLocaleString('ru') + " ₽"
        }), 1000)
    }
}

function shortName(fullName: string): string{
    return fullName.slice(0, fullName.indexOf(' ')) + fullName.slice(fullName.lastIndexOf(' '))
}
function getDay(date: Date): string{
    let months = ['Января','Февраля','Марта','Апреля','Майя','Июня','Июля','Августа','Сентября','Октября','Ноября','Декабря']
    return `${date.getDate()} ${months[date.getMonth()]} ${date.getFullYear()}`
}
</script>

<style scoped>
.row{
    border-bottom: 1px;
}
.row:hover{
    background-color: #e5f7ff;
}
.name{
    width: 600px;
    height: 50px;
    text-align: left;
    padding-left: 50px;
}
.tags{
    padding: 2px;
    margin: 1em;
}
.status{
    width: 200px;
    height: 50px;
    font-size: 10px;
}
span{
    padding: 6px;
    border-radius: 3px;
}
.person{
    width: 200px;
    height: 50px;
}
.create{
    width: 200px;
    height: 50px;
}
.prise{
    width: 200px;
    height: 50px;
}
</style>