<template>
<div class="addItemForm">
    <input v-model="item.name" type="text/">
    <font-awesome-icon icon="plus-square" :class="[item.name ? 'active' : 'inactive', 'plus']" @click="addItem()"></font-awesome-icon>
</div>
</template>

<script>
export default {
    name: "addItemForm",
    data(){
        return{
            item:{
                name:""
            }
        }
    },
    methods:{
        addItem(){
            if(this.item.name === ''){
                return;
            }
            axios.post('/api/items', {
                item:this.item
            }).then(response => {
                if(response.status === 201){
                    this.item.name = "";
                    this.$emit('reloadList');
                }
            }).catch(error=>{
                console.log(error);
            });
        }
    }
}
</script>

<style scoped>
.addItemForm{
    display: flex;
    justify-content: center;
    align-items: center;
}
input{
    background: #f7f7f7;
    border: 0;
    outline: none;
    padding: 5px;
    margin-right: 5px;
    width: 100%;

}

.active{
    cursor: pointer;
    color: #198754;
}

.inactive{
    color: #999999;
}

.plus{
    font-size: 20px;
}

</style>
