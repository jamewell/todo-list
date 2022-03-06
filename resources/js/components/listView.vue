<template>
    <div>
        <ul class="list-group">
            <div v-for="(item, index) in items" :key="index">
                <list-item
                    :item="item"
                    v-on:itemchanged="$emit('reloadlist')"
                />
            </div>
        </ul>
    </div>
</template>

<script>
import listItem from "./listItem.vue"

export default {
    props: ['items'],

    components: {
        listItem
    }
}
</script>