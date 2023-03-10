<template>
<div>
    <div class="item">
        <input type="checkbox" @change="updateCheck" v-model="item.completed">
        <span :class="[item.completed ? 'completed':'',  'itemText']">{{item.name}}</span>
        <button @click="removeItem()" class="trashIcon">
            <font-awesome-icon icon="trash"></font-awesome-icon>
        </button>
    </div>
</div>
</template>

<script>
export default {
    name: "listItem",
    props:['item'],
    methods:{
        updateCheck(){

            axios.put('/api/items/'+this.item.id, {
                item:this.item
            }).then(response => {

                if(response.status === 200){
                    this.$emit('itemChanged');
                }

            }).catch(error=>{
                console.log(error);
            });



        },
        removeItem(){
            axios.delete('/api/items/'+this.item.id, {
                item:this.item
            }).then(response => {
                if(response.status === 200){
                    this.$emit('itemChanged');
                }
            }).catch(error=>{
                console.log(error);
            });
        }
    }
}
</script>

<style scoped>

.completed{
    text-decoration: line-through;
    color: #999999;
}

.itemText{
    width: 100%;
    margin-left: 10px;
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
}


</style>
