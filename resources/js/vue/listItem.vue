<template>
    <div>
        <input type="checkbox" @change='updateCheck()' v-model="item.completed">
        <span :class="[item.completed ? 'completed' : '', 'itemText']" > {{ item.name }}</span>

        <button> <font-awesome-icon icon="trash" class="trashcan" @click="removeItem()"/> </button>
    </div>
</template>

<script>
    export default {
        props : ['item'],
        methods : {
            updateCheck : function(id){
                axios.put('api/items/'+ this.item.id, {
                    item : this.item
                })
                .then(
                    response => {
                        if(response.status == 200){
                            this.$emit('itemchanged');
                        }
                    }
                )
                .catch( error => console.log(error))
            },
            removeItem : function(){
                axios.delete('api/items/'+ this.item.id, {
                    item: this.item
                })
                .then(
                    response => {
                        console.log(response)
                        if(response.status == 200){
                            this.$emit('itemchanged');
                        }
                    }
                )
                .catch(error=>function(){
                    console.log(error)
                })
            }
        }
    }
</script>

<style scoped>
    .completed{
        text-decoration: line-through;
        color:#999999;
    }

    .itemText{
        width: 100%;
        margin-left: 20px;
    }

    .item{
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .trashcan{
        border: none;
        background: #FF0000;
    }
</style>
