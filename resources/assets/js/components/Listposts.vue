<template id="listposts">
    <div class="row">
        <div class="pull-right">
            <router-link class="btn btn-xs btn-primary" v-bind:to="{path: '/add-post'}">

            <span class="glyphicon glyphicon-plus"></span>
                Ajouter Laureat
            </router-link>
        </div>
        <table class="table">
            <thead>
            <tr>
                <th>#</th>
                <th>Laureatt Nom</th>
                <th>Laureat Prenom</th>
                <th>Email</th>
                <th>CNE</th>
                <th class="col-md-2">Actions</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(post, index) in filteredPosts">
                <td>{{ index + 1 }}</td>
                <td>{{ post.nom }}</td>
                <td>{{ post.prenom }}</td>
                <td>{{ post.email }}</td>
                <td>{{ post.cne }}</td>
                <td>

                    <router-link  class="btn btn-info btn-xs" v-bind:to="{name: 'Viewpost', params: {id: post.id}}"><i class="fa fa-eye" aria-hidden="true"></i> Show</router-link>
                    <router-link class="btn btn-warning btn-xs" v-bind:to="{name: 'Editpost', params: {id: post.id}}"><i class="fa fa-pencil" aria-hidden="true"></i> Edit</router-link>
                    <router-link class="btn btn-danger btn-xs" v-bind:to="{name: 'Deletepost', params: {id: post.id}}"><i  class="fa fa-trash-o" aria-hidden="true"></i> Delete</router-link>



                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        components: { },

    data:function(){

            return {posts: ''};
        },
        created: function() {
            let uri = 'http://localhost:8000/laureats/';
            Axios.get(uri).then((response) => {
                this.posts = response.data;
            });
        },
        computed: {
            filteredPosts: function(){
                if(this.posts.length) {
                    return this.posts;
                }
            }
        }
    }


</script>