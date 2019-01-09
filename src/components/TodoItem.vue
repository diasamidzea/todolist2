<template>
    <div>
        <input type="checkbox" v-model="todo.maked"/>
        <item-name :todo="todo" :chooseId="chooseId" @choose="$emit('choose', todo.id)"
                       @change="$emit('change', [$event, index])" @canceled="$emit('canceled')"/>
        <input type="button" value="x" @click="$emit('del')"/>
    </div>
</template>

<script>
    import ItemName from "./ItemName.vue"

    //коментарий для гитхаба
    export default {
        components: {
            ItemName
        },
        props: ["todo", "chooseId", "index"]
    }
</script>
