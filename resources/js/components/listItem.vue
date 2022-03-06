<template>
    <li class="list-group-item">
        <div class="form-check">
            <input type="checkbox" class="form-check-input"
                @change="updateCheck()"
                v-model="item.completed"
            >
            <span class="form-check-label"
                :class="[item.completed ? 'completed' : '', 'itemText']"
            >
                {{ item.name }}
            </span>
            <button class="btn btn-danger float-end"
                @click="removeItem()"
                >
                delete
            </button>
        </div>
    </li>
</template>

<script>
export default {
    props: ['item'],

    methods: {
        updateCheck(){
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then((result) => {
                if(result.status == 200){
                    this.$emit('itemchanged');
                }
            }).catch((err) => {
                console.log(err)
            });
        },

        removeItem() {
            axios.delete('api/item/' + this.item.id)
            .then((result) => {
                if(result.status == 200){
                    this.$emit('itemchanged')
                }
            }).catch((err) => {
                console.log(err)
            });
        }
    }
}
</script>

<style scoped>
.completed {
    text-decoration: line-through;
    color: black;
}
.itemText {
    width: 100%;
    margin-left: 20px;
}
</style>