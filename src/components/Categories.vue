<template>
<div>
    <div v-if="isCatSet" @click="selectCategory(undefined)">
        remove filter
    </div>
    <div>
        <ul>
            <li v-for="category in Categories"
            :key="category"
            @click="selectCategory(category)"
            :class="{selected: category == isCatSet}"
            >
                {{category}}
            </li>

        </ul>
    </div>
</div>
</template>

<script>
export default {
    props: ['Categories'],

    data: () => {
        return {
            isCatSet: undefined,
        }
    },

    methods: {
        selectCategory(category) {
            this.isCatSet = category
            this.$emit('setCategory', category)
        }
    }
}
</script>

<style scoped>
    .selected {
        font-weight: bold;
    }
</style>