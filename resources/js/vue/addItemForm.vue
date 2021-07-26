<template>
    <div class="addItem">
        <input type="text" v-model='item.name'>
        <font-awesome-icon
            @click="addItem()"
            icon="plus-square"
            :class = "[ item.name ? 'active' : 'inactive', 'plus']"
        />
    </div>
</template>

<script>
    export default {
        data : function (){
            return {
               item :  {
                    name : ''
                }
            }
        },
        methods : {
            addItem (){
                if(this.item.name == ''){
                    return;
                }

                axios.post('api/items', {
                    item : this.item
                })
                .then( response =>{

                    if(response.status == 201){
                        this.item.name = ""
                        this.$emit('addeditem')
                    }
                }
                )
                .catch( error => {
                        console.log(error)
                    }
                )

            }
        }
    }
</script>

<style scoped>
    .addItem{
        display: flex;
        justify-content: center;
        align-items: center;
    }

    input{
        background: #f7f7f7;
        border: 0;
        padding: 5px;
        margin-right: 5px;
        margin-left: 5px;
        outline: none;
        width: 100%;
    }

    .active{
        color:green;
        margin-right : 5px;
    }

    .inactive{
        /* color :#999999; */
        color :#CA5454;
        margin-right : 5px;
    }

    .plus{
        font-size:20px;
    }

</style>
