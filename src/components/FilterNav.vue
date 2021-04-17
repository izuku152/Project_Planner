<template>
    <nav class="filter-nav">
        <button
            @click="filterChange('viewall')"
            :class="{ active: current == 'viewall' }"
        >
            View All
        </button>
        <button
            @click="filterChange('ongoing')"
            :class="{ active: current == 'ongoing' }"
        >
            Ongoing
        </button>
        <button
            @click="filterChange('completed')"
            :class="{ active: current == 'completed' }"
        >
            Completed
        </button>
    </nav>
</template>

<script>
export default {
    props: ["current"],
    methods: {
        filterChange(by) {
            this.$emit("change", by);
        },
    },
};
</script>

<style>
.filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}
.filter-nav button.active {
    color: #555;
}
</style>