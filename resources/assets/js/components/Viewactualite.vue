<template id="act">

    <table class="table">
        <thead>
        <tr>
            <th>#</th>
            <th> Titre</th>
            <th>Description</th>
            <th>Image</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td>{{ index + 1 }}</td>
            <td>{{ act.titre }}</td>
            <td>{{ act.description}}</td>
            <td>{{ act.image }}</td>
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
            return {act: {titre: '', description: '',image:''}}
        },
        created: function(){
            let uri = 'http://localhost:8000/actualites/'+this.$route.params.id;
            Axios.get(uri).then((response) => {
                this.act = response.data;
            });
        }
    }
</script>
