<template id="act-edit">
    <div>
        <h3>Modifier l'actualité</h3>
        <form v-on:submit.prevent = "updateAct">
            <div class="form-group">
                <label>Titre</label>
                <input name="titre" v-model="act.titre" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('titre') }"
                       type="text" placeholder="titre">
                <i v-show="errors.has('titre')" class="fa fa-warning"></i>
                <span v-show="errors.has('titre')" class="" style="color: red">{{ errors.first('titre') }}</span>

            </div>
            <div class="form-group">
                <label>Description</label>
                <input name="description" v-model="act.description" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('description') }"
                       type="text" placeholder="description">
                <i v-show="errors.has('description')" class="fa fa-warning"></i>
                <span v-show="errors.has('description')" class="" style="color: red">{{ errors.first('description') }}</span>

            </div>
            <div class="form-group">
                <label>Image</label>
                <input name="titre" v-model="act.image" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('image') }"
                       type="text" placeholder="image">
            </div>
            <button type="submit" class="btn btn-xs btn-primary">Modifier</button>
            <router-link class="btn btn-xs btn-warning" v-bind:to="'/'">Cancel</router-link>
        </form>
    </div>
</template>
<script>
    export default{
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
            updateAct: function() {
                let uri = 'http://localhost:8000/actualites/'+this.$route.params.id;
                Axios.patch(uri, this.act).then((response) => {
                    this.$router.push({name: 'Listacts'})
                })
            }
        }
    }
</script>


