<template>
    <div class="home">
        <FilterNav @change="current = $event" :current="current" />
        <div v-if="projects.length">
            <div v-for="project in filteredProjects" :key="project.id">
                <SingleProject
                    :project="project"
                    @delete="handleDelete"
                    @complete="handleComplete"
                />
            </div>
        </div>
    </div>
</template>

<script>
import SingleProject from "../components/SingleProject";
import FilterNav from "../components/FilterNav";
export default {
    components: { SingleProject, FilterNav },
    data() {
        return {
            url: "http://localhost:3000/projects/",
            projects: [],
            current: "viewall",
        };
    },
    methods: {
        handleDelete(id) {
            this.projects = this.projects.filter((project) => {
                return project.id !== id;
            });
        },
        handleComplete(id) {
            let p = this.projects.find((project) => project.id == id);
            p.isCompleted = !p.isCompleted;
        },
    },
    computed: {
        filteredProjects() {
            let filtered = this.projects;
            if (this.current == "completed") {
                filtered = this.projects.filter((project) => {
                    return project.isCompleted !== false;
                });
            } else if (this.current == "ongoing") {
                filtered = this.projects.filter((project) => {
                    return project.isCompleted !== true;
                });
            } else if (this.current == "viewall") {
                filtered = this.projects.filter((project) => {
                    return project;
                });
            }
            return filtered;
        },
    },
    mounted() {
        // Fetching Data from Data/DB.json
        fetch(this.url)
            .then((res) => res.json())
            .then((data) => (this.projects = data))
            .catch((err) => console.log(err.message));
    },
};
</script>

<style></style>
