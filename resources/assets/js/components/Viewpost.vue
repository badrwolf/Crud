<template id="post">

    <table class="table">
        <thead>
        <tr>
            <th>#</th>
            <th> Nom</th>
            <th>Prenom</th>
            <th>Email</th>
            <th>CNE</th>
            <th>CIN</th>
            <th>Téléphone</th>
            <th>Promotion</th>
            <th>Nationalité</th>
            <th>Pays</th>
            <th>Ville</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td>{{ index}}</td>
            <td>{{ post.nom }}</td>
            <td>{{ post.prenom }}</td>
            <td>{{ post.email }}</td>
            <td>{{ post.cne }}</td>
            <td>{{ post.cin }}</td>
            <td>{{ post.telephone }}</td>
            <td>{{ post.promo }}</td>
            <td>{{ post.nationalite }}</td>
            <td>{{ post.pays }}</td>
            <td>{{ post.ville }}</td>
            <td>
                <span class="glyphicon glyphicon-arrow-left"></span>
                <router-link v-bind:to="'/'">revenir</router-link>
            </td>
        </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        data: function () {
            return {post: {nom: '', prenom: '',email:'',cne:'',cin:'',telephone:'',promo:'',nationalite:'',pays:'',ville:''}}
        },
        created: function(){
            let uri = 'http://localhost:8000/laureats/'+this.$route.params.id;
            Axios.get(uri).then((response) => {
                this.post = response.data;
            });
        }
    }
</script>
