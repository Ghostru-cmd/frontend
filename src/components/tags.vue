<template>
    <span class="tag">{{tag}}</span>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component({
    props: {
        tag: String
    }
})

export default class Tags extends Vue {
    
}
</script>

<style scoped>
.tag{
    background-color: rgb(158 158 158 / 30%);
    padding: 4px;
    border-radius: 3px;
    margin: 2px;
}
</style>