<template>
    <div class="card card-body mb-2">
        <div class="row">
            <div class="col-md-5">
                <a :href="repository.html_url" target="_blank"> <strong>{{repository.full_name}}</strong></a>
            </div>
            <div class="col-md-7">
                <span v-if="repository.language" class="badge badge-secondary">
                    <i class="fa fa-circle"></i> {{repository.language}}
                </span>
                <span class="badge badge-custom">
                    <i class="fa fa-star"></i> {{repository.stargazers_count}}
                </span>
                <span class="badge badge-primary">
                    <i class="fa fa-eye"></i> {{repository.watchers_count}}
                </span>
                <span class="badge badge-secondary">
                    <i class="fa fa-code-branch"></i> {{repository.forks_count}}
                </span>          
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