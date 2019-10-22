<template>
    <div class="card card-body mb-2">
        <div class="row">
            <div class="col-md-6">
                <a :href="repository.html_url" target="_blank"> {{repository.name}}</a>
            </div>
            <div class="col-md-6">
                <span class="badge badge-custom">Stars: {{repository.stargazers_count}}</span>
                <span class="badge badge-primary">Watchers: {{repository.watchers_count}}</span>
                <span class="badge badge-secondary">Forks: {{repository.forks_count}}</span>          
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['repository']
}
</script>

<style>
    .btn-custom {
        background: #3FB984;
        color: #fff;
    }

    .badge-custom {
        background: #3FB984;
        color: #fff;
    }

    .badge {
        margin-left: 8px;
    }
</style>