<template id="post-edit">
    <div>
        <h3>Ajouter laureat</h3>
        <form v-on:submit.prevent = "updatePost">
            <div class="form-group">
                <label>Nom</label>
                <input name="nom" v-model="post.nom" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('nom') }"
                       type="text" placeholder="Nom">
                <i v-show="errors.has('nom')" class="fa fa-warning"></i>
                <span v-show="errors.has('nom')" class="" style="color: red">{{ errors.first('nom') }}</span>

            </div>
            <div class="form-group">
                <label >Prenom</label>
                <input class="form-control"  v-model="post.prenom" required></input>
            </div>

            <div class="form-group">
                <label >CNE</label>
                <input name="cne" v-model="post.cne" v-validate="'required|numeric'" :class="{'input': true, 'is-danger': errors.has('cne') }"
                       type="text" placeholder="CNE">
                <i v-show="errors.has('cne')" class="fa fa-warning"></i>
                <span v-show="errors.has('cne')" class="" style="color: red">{{ errors.first('cne') }}</span>

            </div>

            <div class="form-group">
                <label >Email</label>
                <input class="form-control"  v-model="post.email" required
                       v-validate="'required|email'" :class="{'input': true, 'is-danger': errors.has('email') }" name="email" type="text" placeholder="Email">
                <span v-show="errors.has('email')" style="color: red" class="help is-danger">{{ errors.first('email') }}</span>
            </div>

            <div class="form-group">
                <label >CIN</label>
                <input class="form-control"  v-model="post.cin" required
                       v-validate="'required|alpha_num'" :class="{'input': true, 'is-danger': errors.has('cin') }" name="cin" type="text" placeholder="CIN">
                <span v-show="errors.has('cin')" class="help is-danger">{{ errors.first('cin') }}</span>
            </div>
            <div class="form-group">
                <label >Télephone</label>
                <input name="telephone" v-model="post.telephone" v-validate="'required|numeric'" :class="{'input': true, 'is-danger': errors.has('telephone') }"
                       type="text" placeholder="Téléphone">
                <i v-show="errors.has('telephone')" class="fa fa-warning"></i>
                <span v-show="errors.has('telephone')" class="" style="color: red">{{ errors.first('telephone') }}</span>
            </div>
            <div class="form-group">
                <label >Promotion</label>
                <select v-model="post.promo">
                    <option SELECTED>2013</option>
                    <option>2014</option>
                    <option>2015</option>
                    <option>2016</option>
                    <option>2017</option>
                    <option>2018</option>
                </select>
            </div>

            <div class="form-group">
                <label >Nationalité</label>
                <input name="nationalite" v-model="post.nationalite" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('nationalite') }"
                       type="text" placeholder="nationalite">
                <i v-show="errors.has('nationalite')" class="fa fa-warning"></i>
                <span v-show="errors.has('nationalite')" class="" style="color: red">{{ errors.first('nationalite') }}</span>
            </div>
            <div class="form-group">
                <label >Pays</label>
                <input name="pays" v-model="post.pays" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('pays') }"
                       type="text" placeholder="pays">
                <i v-show="errors.has('pays')" class="fa fa-warning"></i>
                <span v-show="errors.has('pays')" class="" style="color: red">{{ errors.first('pays') }}</span>
            </div>
            <div class="form-group">
                <label >Ville</label>
                <input name="ville" v-model="post.ville" v-validate="'required|alpha'" :class="{'input': true, 'is-danger': errors.has('ville') }"
                       type="text" placeholder="ville">
                <i v-show="errors.has('ville')" class="fa fa-warning"></i>
                <span v-show="errors.has('ville')" class="" style="color: red">{{ errors.first('ville') }}</span>
            </div>

            <button type="submit" class="btn btn-xs btn-primary">Modifier</button>
            <router-link class="btn btn-xs btn-warning" v-bind:to="'/'">Annuler</router-link>
        </form>
    </div>
</template>

<script>
    export default{
        data: function () {
            return {post: {nom: '', prenom: '',email:'',cne:'',cin:'',telephone:'',promo:'',nationalite:'',pays:'',ville:''}}
        },
        created: function(){
            let uri = 'http://localhost:8000/laureats/'+this.$route.params.id+'/edit';
            Axios.get(uri).then((response) => {
                this.post = response.data;
            });
        },
        methods: {
            updatePost: function() {
                let uri = 'http://localhost:8000/laureats/'+this.$route.params.id;
                Axios.patch(uri, this.post).then((response) => {
                    this.$router.push({name: 'Listposts'})
                })
            }
        }
    }
</script>
