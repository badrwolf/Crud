<template id="post-delete">
    <div class="center">
        <h3>Supprimer le laureat {{ post.nom  }}</h3>
        <form v-on:submit.prevent = "deletePost">
            <p>êtes vous sure</p>
            <button class="btn btn-xs btn-danger" type="submit" name="button">Supprimer</button>
            <router-link class="btn btn-xs btn-primary" v-bind:to="'/'">Revenir</router-link>
        </form>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {post: {nom: '', prenom: '',cne:'',cin:'',telephone:'',promo:'',nationalite:'',pays:'',ville:''}}
        },
        created: function(){
            let uri = 'http://localhost:8000/laureats/'+this.$route.params.id+'/edit';
            Axios.get(uri).then((response) => {
                this.post = response.data;
            });
        },
        methods: {
            deletePost: function() {
                let uri = 'http://localhost:8000/laureats/'+this.$route.params.id;
                Axios.delete(uri, this.post).then((response) => {
                    this.$router.push({name: 'Listposts'})
                })
            }
        }
    }
</script>
.center {
margin: auto;
width: 50%;
border: 3px solid green;
padding: 10px;
}