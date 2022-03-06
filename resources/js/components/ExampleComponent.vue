<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">
                        <h3>Todo List</h3>
                    </div>

                    <div class="card-body">
                        <add-item-form 
                            v-on:reloadlist="getList()"
                        />
                        <list-view 
                            :items="items"
                            v-on:reloadlist="getList()"
                            />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import addItemForm from "./addItemForm.vue"
    import listView from "./listView.vue"
    
    export default {
        mounted() {
            console.log('Component mounted.')
        },

        components: {
            addItemForm,
            listView
        },

        data: function() {
            return {
                items: []
            }
        },

        methods: {
            getList() {
                axios.get('api/items')
                .then((result) => {
                    this.items = result.data
                }).catch((err) => {
                    console.log(err)
                });
            }
        },

        created() {
            this.getList();
        }
    }
</script>

<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
}

</style>