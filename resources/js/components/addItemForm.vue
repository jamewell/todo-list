<template>
    <div class="input-group mb-3">
        <input type="text" class="form-control" v-model="item.name">
        <button class="btn btn-outline-secondary" 
            :class="[ item.name ? 'btn-outline-success' : 'btn-outline-secondary' ]"
            @click="addItem()">
            <font-awesome-icon icon="fa-regular fa-plus" />
        </button>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        }
    },

    methods: {
        addItem() {
            if(this.item.name == ''){
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then((result) => {
                if(result.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            }).catch((err) => {
                console.log(err)
            });
        }
    }
}
</script>

<style scoped>
.active {
    color: #00CE25;
}

.inactive {
    color: #999999;
}
</style>