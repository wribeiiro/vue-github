<template>
    <div id="app">
        <Navbar/>
        <div class="container">
            <div class="card card-body">
                <h1>Search in github</h1>
                <p class="lead">Type something for searching</p>
                <input id="search" type="text" class="form-control" required @keyup="getInfo" placeholder="Waiting for search..."/>
            </div>

            <div class="row mt-3" v-if="users.length !== 0">
                <div class="col-md-4">
                    <ProfileUser :user="users"/>
                </div>

                <div class="col-md-8" v-if="repositories.length !== 0">
                    <RepositoriesUser v-for="(repo, index) in repositories" :key="index+10" :repository="repo"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import ProfileUser from "./components/ProfileUser.vue";
import RepositoriesUser from "./components/RepositoriesUser.vue";
import axios from "axios";

export default {
    name: 'app',
    data() {
        return {
            params: {
                url: 'https://api.github.com/users',
                client_id: '0bbeff79fa0c5d3f9e01',
                client_secret: '73699f371e3fb06074c17ad064f064d82d29443c',
                per_page: 100,
                sort: 'created:asc'
            },
            users: [],
            repositories: []
        }
    },
    components: {
        Navbar,
        ProfileUser,
        RepositoriesUser
    },
    methods: {
        getRepositories(user) {
            axios.get(
                `${this.params.url}/${user}/repos?per_page=${this.params.per_page}&sort=${this.params.sort}&client_id=${this.params.client_id}&client_secret=${this.params.client_secret}`
            )
            .then(({data}) => {
                this.repositories = data;
            })
            .catch(() => {
                this.repositories = [];
            }); 
        },
        getProfile(user) {
            axios.get(
                `${this.params.url}/${user}?client_id=${this.params.client_id}&client_secret=${this.params.client_secret}`
            ).then(({data}) => {
                this.users = data;
            }).catch(() => {
                this.users = [];
            });
        },
        getInfo(value) { 
            const user = value.target.value;

            if(user.length) {
                this.getProfile(user);
                this.getRepositories(user);
            } else {
                this.users        = [];
                this.repositories = [];
            }
        }
    }
}
</script>

<style></style>