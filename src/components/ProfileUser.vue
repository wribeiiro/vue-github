<template>
    <div class="row form-group">
        <div class="col-md-4">
            <div class="card" style="width: 18rem">
                <img class="card-img-top" :src="user.avatar_url" alt="">
                <ul class="list-group list-group-flush">
                    <li class="list-group-item"><strong>{{user.name}}</strong></li>
                    <li class="list-group-item">Repositories <span class="badge badge-custom">{{user.public_repos}}</span></li>
                    <li class="list-group-item">Followers <span class="badge badge-primary">{{user.followers}}</span></li>
                    <li class="list-group-item">Following <span class="badge badge-info">{{user.following}}</span></li>
                </ul>
                <div class="card-body">
                    <a :href="user.html_url" class="btn btn-custom btn-block">View profile</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['user']
}
</script>

<style>
    .card,
    .list-group,
    .list-group-item {
        background: #212025;
    }

    .btn-custom {
        background: #9466FF !important;
        color: #fff;
    }

    .badge-custom {
        background: #9466FF;
        color: #fff;
    }
</style>