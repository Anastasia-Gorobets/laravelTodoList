<template>
<div class="todoListContainer">
    <div class="heading">
        <h2 id="title">Todo List</h2>
        <add-item-form v-on:reloadList="getList()"></add-item-form>
        <list-view :items="items" v-on:reloadList="getList()"></list-view>
    </div>
</div>
</template>
<script>
import addItemForm from './addItemForm';
import listView from './listView';
export default {
    components:{addItemForm,listView},
    name: "app",
    data(){
        return{
           items:[]
        }
    },
    methods:{
        getList(){
            axios.get('/api/items', {
                item:this.item
            }).then(response => {
                this.items = response.data;
            }).catch(error=>{
                console.log(error);
            });
        }
    },
    created() {
        this.getList();
    }
}
</script>

<style scoped>
.todoListContainer{
    width:400px;
    margin:auto;
}
.heading{
    background: #e6e6e6;
    padding:10px
}
#title{
    text-align: center;
}
</style>
