<template>
    <div class="project" :class="project.isCompleted == true ? 'complete' : ''">
        <div class="actions">
            <h2
                :class="project.isCompleted ? 'complete' : 'false'"
                @click="handleClick"
            >
                {{ project.title }}
            </h2>
            <div class="icons">
                <router-link :to="{ name: 'Edit', params: { id: project.id } }">
                    <span class="material-icons edit" @click="editTodo">
                        edit
                    </span>
                </router-link>
                <span class="material-icons del" @click="deleteTodo"
                    >delete</span
                >
                <span class="material-icons tick" @click="completeTodo"
                    >done</span
                >
            </div>
        </div>
        <div class="details">
            <p v-if="showDetails">{{ project.details }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ["project"],
    data() {
        return {
            showDetails: false,
            url: "http://localhost:3000/projects/" + this.project.id,
        };
    },
    methods: {
        handleClick() {
            this.showDetails = !this.showDetails;
        },
        //   Delete
        deleteTodo() {
            fetch(this.url, { method: "DELETE" })
                .then(() => this.$emit("delete", this.project.id))
                .catch((err) => console.log(err.message));
        },
        //   Done
        completeTodo() {
            fetch(this.url, {
                method: "PATCH",
                headers: { "Content-type": "application/json" },
                body: JSON.stringify({
                    isCompleted: !this.project.isCompleted,
                }),
            }).then(() => this.$emit("complete", this.project.id));
        },
    },
};
</script>

<style>
.project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
    border-left: 4px solid #e90074;
    user-select: none;
}
h3 {
    cursor: pointer;
    /* user-select: none; */
}
.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}
.material-icons:hover {
    color: #777;
}
/* completed projects */
.project.complete {
    border-left: 4px solid #00ce89;
}
.project.complete .tick {
    color: #00ce89;
}
.project .tick:hover {
    color: #00ce89;
}
.project .del:hover {
    color: #e90074;
}
.project .edit:hover {
    color: #ff9800;
}
</style>