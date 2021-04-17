<template>
    <form @submit.prevent="handleSubmit" v-if="typeof project != 'undefined'">
        <label>Title: </label>
        <input type="text" v-model="project.title" required />
        <label>Details: </label>
        <textarea v-model="project.details" required></textarea>
        <button>Add Todo</button>
    </form>
</template>

<script>
export default {
    props: ["id"],
    data() {
        return {
            project: {},
            url: "http://localhost:3000/projects/" + this.id,
        };
    },
    methods: {
        handleSubmit() {
            fetch(this.url, {
                method: "PATCH",
                headers: { "Content-type": "application/json" },
                body: JSON.stringify(this.project),
            }).then(() => this.$router.push("/"));
        },
    },
    mounted() {
        fetch(this.url)
            .then((res) => res.json())
            .then((data) => (this.project = data))
            .then(() => console.log(this.project))
            .catch((err) => console.log(err.message));
    },
};
</script>

<style>
</style>