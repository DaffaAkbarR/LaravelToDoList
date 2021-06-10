<template>
    <div class="addContent">
        <input type="text" v-model="content.name"/>
        <font-awesome-icon
            icon="plus-square"
            @click="addContent"
            :class="[ content.name ? 'active' : 'inactive', 'plus']"
        />
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            content: {
                name: ""
            }
        }
    },
    methods: {
        addContent() {
            if(this.content.name == '') {
                return;
            }

            axios.post('api/content/store', {
                content: this.content
            })
            .then( response => {
                if(response.status == 201) {
                    this.content.name = "";
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
.addContent {
    display: flex;
    justify-content: center;
    align-items: center;
}
input {
    background: white;
    border: 0px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}
.plus {
    font-size: 20px;
}
.active {
    color: rgb(4, 153, 4);
}
.inactive {
    color: rgb(31, 30, 30);
}
</style>
