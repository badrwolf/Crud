<template id="act-delete">
    <div class="center">
        <h3>Supprimer l'actualité: {{ act.titre }}</h3>
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
            return {act: {titre: '', description: '',image:''}}
        },
        created: function(){
            let uri = 'http://localhost:8000/actualites/'+this.$route.params.id+'/edit';
            Axios.get(uri).then((response) => {
                this.act = response.data;
            });
        },
        methods: {
            deletePost: function() {
                let uri = 'http://localhost:8000/actualites/'+this.$route.params.id;
                Axios.delete(uri, this.act).then((response) => {
                    this.$router.push({name: 'Listacts'})
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