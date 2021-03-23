<template>
    <tr class='row' :id="i">
        <th class='name'>{{contact.name}}</th>
        <th class='phone'>{{phoneEmail[0]}}</th>
        <th class='email'>{{phoneEmail[1]}}</th>
    </tr>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

interface State {
    phoneEmail: any
}

@Component({
  components: {
  },
  props: {
        i: Number,
        contact: Object
    }
})

export default class RowContact extends Vue {
    contact!: any
    phoneEmail!: Array<string>

    data(): State {
        return {
            phoneEmail: []
        }
    }
    mounted(): void {
        this.phoneEmail = this.contact.custom_fields_values.map((phoneEmail: any) => phoneEmail.values[0].value)
    }
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