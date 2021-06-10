<template>
    <div class="todoContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-content-form />
        </div>
        <list-view
            :contents="contents"
            v-on:reloadlist="getList()"
         />
    </div>
</template>

<script>
import addContentForm from './addContentForm'
import listView from "./listView"

export default {
  components: {
      addContentForm,
      listView
  },
  data: function () {
      return {
          contents: []
      }
  },
  methods: {
      getList () {
          axios.get('api/contents')
          .then(response => {
              this.contents = response.data
          })
          .catch(error => {
              console.log(error);
          })
      }
  },
  created() {
      this.getList();
  }

}
</script>

<style scoped>
.todoContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: rgb(185, 185, 185);
    padding: 10px;
}

#title {
    text-align:center;
}
</style>
