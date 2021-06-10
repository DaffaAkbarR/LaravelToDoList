<template>
    <div class="content">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="content.finished"
        />
        <span :class="[content.finished ? 'finished' : 'contentText']"></span>
        <button @click="removeContent()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ['content'],
    methods: {
        updateCheck() {
            axios.put('api/content/' + this.content.id, {
                content: this.content
            })
            .then (responses => {
                if (response.status == 200) {
                    this.$emit('itemchanged');
                }
            })
            .catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.complete {
    text-decoration: line-through;
    color: #721919;
}
.contentText {
    width: 100%;
    margin-left: 20px;
}
.content {
    display: flex;
    justify-content: center;
    align-items: center;
}
.trashcan {
    background: rgb(189, 189, 189);
    border: none;
    color: rgb(134, 14, 14);
    outline: none;
}
</style>
