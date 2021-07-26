<template>
    <div class="bigContainer">
        <div class="heading">
            <h2 id="title">TodoList</h2>
            <add-item-form v-on:addeditem="getListItem()"/>
        </div>

        <list-view :items="items" v-on:reloadlist="getListItem()"/>

    </div>
</template>

<script>
    import addItemForm from './addItemForm';
    import listView from './listView';

    export default{
        components : {
            addItemForm,
            listView
        },
        data : function(){
            return {
                items : []
            }
        },
        methods : {
            getListItem () {
                axios.get('api/items')
                .then( response => {
                    console.log(response.data)
                    this.items = response.data
                })
                .catch(
                    error => {
                        console.log(error)
                    }
                )
            }
        },
        created(){
            this.getListItem()
        }
    }
</script>

<style scoped>
    .bigContainer{
        width : 400px;
        margin: auto;
        background: #e6e6e6;
    }

    #title{
        text-align: center;
        padding: 5px;
    }

    .list-item{
        margin-top: 20px;
        background-color: yellow;
    }
</style>
