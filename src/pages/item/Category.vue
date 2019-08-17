<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        console.log(node);
        this.$http.post("/item/category",node).then(resp=>{
          /*this.$http.get("/item/category/list").then(resps=>{
            console.log("resps=========>"+resps);
          });*/
          this.$message.success("保存成功");
        }).catch(()=>{
          this.$message.error('保存失败');
        })
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name)
        this.$http.put("/item/category",{id:id,name:name}).then(resp=>{
          console.log(resp);
          this.$message.success("更新成功");
        }).catch(()=>{
          this.$message.error('更新失败');
        })
      },
      handleDelete(id) {
        console.log("delete ... " + id);
        this.$http.delete("/item/category/"+id).then(resp=>{
          console.log(resp);
        })
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
