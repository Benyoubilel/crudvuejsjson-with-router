<script setup lang="ts">
</script>

<template>
    <!-- Button trigger modal -->


    <!-- AddModal -->
    <section class="container-fluid p-4">
        <div class="row dark">
            <div class="col-md-12">
                <div class="container-fluid p-4">
                    <form class="form-floating" method="POST">

                        <div class="modal-body">
                            <label class="p-2">nom</label>
                            <input type="text" class="form-control" name="nom" id="nom" placeholder="ali" v-model="nom">

                            <label class="p-2">prenom</label>
                            <input type="text" class="form-control" name="prenom" id="prenom" placeholder="benali" v-model="prenom">
                            <div class="modal-footer m-2">
                                
                                <button type="submit" v-on:click="addUsr()" class="btn btn-success" id="submit">Ajouter</button>
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
import { required, email, minLength } from "@vuelidate/validators";
export default {
    name: 'ajouter',
    data() {
        return {
            user: [{
                "nom": "",
                "prenom": "",
                "id": "",
            }
            ],
            v$: useValidate(),
            id: "",
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
        async addUsr() {
            this.v$.$validate();
            if (!this.v$.$error) {
                console.log("valid??");
                let result = await axios.post('http://localhost:3000/user', {
                    nom: this.nom,
                    prenom: this.prenom,
                });
            }
            window.location.href = "/"
        }


    },

};
</script>