<template>
<div>
    <div v-for="(item,index) in items" :key="index">
        <list-item :item="item" class="item" v-on:itemChanged="itemChanged()"></list-item>
    </div>
</div>
</template>

<script>
import listItem from './listItem';
export default {
    name: "listView",
    props:['items'],
    components:{listItem},
    methods:{
        itemChanged(){
            this.$emit('reloadList');
        }
    }
}
</script>

<style scoped>
.item{
    background: #e6e6e6;
    padding: 5px;
    margin: 5px;
}

</style>
