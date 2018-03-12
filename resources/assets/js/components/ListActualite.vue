<template id="Listacts">
    <div class="row">
        <div class="pull-right">
            <router-link class="btn btn-xs btn-primary" v-bind:to="{path: '/add-act'}">

                <span class="glyphicon glyphicon-plus"></span>
                Ajouter Actualité
            </router-link>
        </div>
        <table class="table">
            <thead>
            <tr>
                <th>#</th>
                <th>Titre</th>
                <th>Description</th>
                <th>Image</th>
                <th class="col-md-2">Actions</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(act, index) in filteredActs">
                <td>{{ index + 1 }}</td>
                <td>{{ act.titre }}</td>
                <td>{{ act.description }}</td>
                <td><img :src="'http://localhost:8000/'+act.image"/></td>
                <td>

                    <router-link  class="btn btn-info btn-xs" v-bind:to="{name: 'Viewact', params: {id: act.id}}"><i class="fa fa-eye" aria-hidden="true"></i> Show</router-link>
                    <router-link class="btn btn-warning btn-xs" v-bind:to="{name: 'Editact', params: {id: act.id}}"><i class="fa fa-pencil" aria-hidden="true"></i> Edit</router-link>
                    <router-link class="btn btn-danger btn-xs" v-bind:to="{name: 'Deleteact', params: {id: act.id}}"><i  class="fa fa-trash-o" aria-hidden="true"></i> Delete</router-link>



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

            return {acts: ''};
        },
        created: function() {
            let uri = 'http://localhost:8000/actualites/';
            Axios.get(uri).then((response) => {
                this.acts = response.data;
            });
        },
        computed: {
            filteredActs: function(){
                if(this.acts.length) {
                    return this.acts;
                }
            }
        }
    }


</script>