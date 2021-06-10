<template>
    <div>
        <div v-for="(content, index) in contents" :key="index">
            <list-content
                :content="content"
                class="content"
                v-on:itemchanged="$emit('reloadlist')"
                />

        </div>
    </div>
</template>

<script>
import listContent from "./listContent"
import ListContent from './listContent.vue'

export default {
    props: ['contents'],
    components: {
        listContent,
        ListContent
    }

}
</script>


<style scoped>
.content {
    background: rgb(189, 189, 189);
    padding: 5px;
    margin-top: 5px;
}
</style>
