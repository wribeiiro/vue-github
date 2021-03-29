<template>
    <div id="app">
        <Navbar/>
        <div class="container">
            <div class="card card-body">
                <h2 class="mb-2 text-center">Search in github</h2>
                <div class="input-group">
                    <div class="input-group-prepend">
                        <span class="input-group-text bg-custom">
                            <i class="fa fa-search"></i>
                        </span>
                    </div>

                    <input id="search" type="text" class="form-control" required @keyup="debounceSearch($event)" placeholder="Waiting for search (repositories, users...)"/>
                </div>
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
import _ from 'lodash';

export default {
    name: 'app',
    data() {
        return {
            params: {
                url: 'https://api.github.com/users',
                client_id: '0bbeff79fa0c5d3f9e01',
                client_secret: '73699f371e3fb06074c17ad064f064d82d29443c',
                per_page: 100,
                sort: 'created:asc',
                debounceSearch: null
            },
            users: [],
            repositories: []
        }
    },
    created() {
        this.debounceSearch = _.debounce(this.getInfo, 100);
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
        getInfo($event) { 
            const user = $event.target.value;
            
            this.users        = [];
            this.repositories = [];

            if (user.length) {
                this.getProfile(user);
                this.getRepositories(user);
            } 
        }
    }
}
</script>

<style>
    body {
        background: #121214;
    }

    .card {
        background: #212025;
        color: #fff;
    }

    #id:active, 
    #id:focus {
        box-shadow: none;
        border: none;
        outline: none;
    }

    .bg-custom {
        background: #9466FF;
        color: #fff;
    }

    input {
        outline: none;
        box-shadow:none !important;
    }

</style>