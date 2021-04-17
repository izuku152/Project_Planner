<template>
    <form @submit.prevent="handleSubmit">
        <label>Title: </label>
        <input type="text" v-model="title" required />
        <label>Details: </label>
        <textarea v-model="details" required></textarea>
        <button>Add Todo</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: "",
            details: "",
            url: "http://localhost:3000/projects/",
        };
    },
    methods: {
        handleSubmit() {
            let project = {
                title: this.title,
                details: this.details,
                isCompleted: false,
            };

            fetch(this.url, {
                method: "POST",
                headers: { "Content-type": "application/json" },
                body: JSON.stringify(project),
            })
                .then(() => this.$router.push("/"))
                .catch((err) => console.log(err.message));
        },
    },
};
</script>

<style>
form {
    background: white;
    padding: 20px;
    margin-top: 50px;
    border-radius: 10px;
}
label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
}
input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
    outline: none;
    transition: 0.3s ease-in-out;
}
input:focus {
    border-bottom: 1px solid #00ce89;
}
textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
    outline: none;
    transition: 0.3s ease-in-out;
}
textarea:focus {
    border: 1px solid #00ce89;
}
form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
}
</style>