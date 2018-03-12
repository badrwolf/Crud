<template id="add-act">
    <div>
        <h3>Ajouter laureat</h3>
        <form v-on:submit.prevent = "createAct">
            <div class="form-group">
                <label>Titre</label>
                <input name="titre" v-model="post.titre" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('titre') }"
                       type="text" placeholder="titre">
                <i v-show="errors.has('titre')" class="fa fa-warning"></i>
                <span v-show="errors.has('titre')" class="" style="color: red">{{ errors.first('titre') }}</span>

            </div>
            <div class="form-group">
                <label>Description</label>
                <input name="description" v-model="post.description" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('description') }"
                       type="text" placeholder="description">
                <i v-show="errors.has('description')" class="fa fa-warning"></i>
                <span v-show="errors.has('description')" class="" style="color: red">{{ errors.first('description') }}</span>

            </div>
            <div class="form-group">
                <label>Image</label>
                <input type="file" @change="imageChanged" class="form-control">
            </div>
            <button type="submit" class="btn btn-xs btn-primary">Créer Actualité</button>
            <router-link class="btn btn-xs btn-warning" v-bind:to="'/'">Cancel</router-link>
        </form>
    </div>
</template>
<script>
    import Vue from 'vue';
    import VeeValidate from 'vee-validate';

    Vue.use(VeeValidate);
    export default {
        data: function () {

            return {post: {titre: '', description: '',image:''}}

        },
        methods: {


            createAct: function() {
                let uri = 'http://localhost:8000/actualites/';
                Axios.post(uri, this.post).then((response) => {
                    this.$router.push({name: 'Listacts'})
                })

            },
            imageChanged(e){
                console.log(e.target.files[0])
                var fileReader=new FileReader()
                fileReader.readAsDataURL(e.target.files[0])
                fileReader.onload=(e)=>{
                    this.post.image=e.target.result
                }
                console.log(this.post)
            }

        }
    }
</script>


