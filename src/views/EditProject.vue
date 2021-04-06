<template>
    <h1>Edit Project</h1>
    <form @submit.prevent="handleSubmit">
        <label>Title</label>
        <input type="text" required v-model="title" />
        <label>Details</label>
        <textarea v-model="details" required></textarea>
        <button>Add Project</button>
    </form>
</template>

<script>
export default {
    props: ["id"],
    data() {
        return {
            title: "",
            details: "",
            uri: "http://localhost:3000/projects/" + this.id,
        };
    },
    methods:{
        handleSubmit(){
            fetch(this.uri,
            {method: 'PATCH',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({title: this.title, details: this.details})
        }).then(()=> this.$router.push('/'))
        }
    },
    mounted() {
        fetch(this.uri)
            .then((res) => res.json())
            .then((data) => {
                console.log(data);
                this.title = data.title;
                this.details = data.details;
            })
            .catch((err) => console.log(err));
    },
};
</script>

<style>
</style>