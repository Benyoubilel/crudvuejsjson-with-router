<script setup lang="ts">
</script>

<template>
    <!-- Button trigger modal -->


    <!-- AddModal -->
    <section class="container-fluid p-4" v-on:load="getusr()">
        <div class="row dark">
            <div class="col-md-12">
                <div class="container-fluid p-4">
                    <form class="form-floating" method="POST">

                        <div class="modal-body">
                            <label class="p-2">nom</label>
                            <input type="text" class="form-control" name="nom" id="nom" placeholder="ali" v-model="nom">

                            <label class="p-2">prenom</label>
                            <input type="text" class="form-control" name="prenom" id="prenom" placeholder="benali"
                                v-model="prenom" >
                            <div class="modal-footer m-2">
                                <button type="button" class="btn btn-danger m-2"
                                    data-bs-dismiss="modal">Annuler</button>
                                <button type="submit" v-on:click="updateUsr(nom,prenom)" class="btn btn-success" id="submit">modifier</button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </section>


</template>
<script>
import axios from "axios";
import useValidate from "@vuelidate/core";
import { required,  minLength } from "@vuelidate/validators";
export default {
    name: 'modifier',
    data() {
        return {
            user: [{
                "nom": "",
                "prenom": "",
            }
            ], 
            v$: useValidate(),
            nom: "",
            prenom: "",
        };
    },
    validattion() {
        return {
            nom: { required, minLength: minLength(3) },
            prenom: { required, minLength: minLength(3) },
        };
    },
    async mounted() {
        let res = await axios.get('http://localhost:3000/user');
        this.user = res.data;
    },
    methods: {
        async updateUsr( nom, prenom) {

            //   let rep=  await axios.get('http://localhost:3000/user/' + id);
            //   this.user= rep.data;
            let rep = await axios.put('http://localhost:3000/user/' + this.id, { nom: nom, prenom: prenom });
            window.location.href = "/"
        },
        async getusr() {
            let res = await axios.get('http://localhost:3000/user/' + this.id);
            this.user = res.data;
        },


    },

};
</script>