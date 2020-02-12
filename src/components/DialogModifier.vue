<template>
    <div>
          <b-modal id="modal-modifier" centered title="BootstrapVue" >
            <h2>Formulaire d'ajout</h2>
            <form>
                <div class="form-group">
                    <label for="biere_nom">Nom de le bière</label>
                    <input v-model="biere.nom" type="text" class="form-control"  aria-describedby="emailHelp" placeholder="Entrer le nom de la bière">
                </div>
                <div class="form-group">
                    <label for="biere_brasserie">Brasserie</label>
                    <input v-model="biere.brasserie" type="text" class="form-control"  aria-describedby="emailHelp" placeholder="Entrer la nom de la brasserie">
                </div>
                <div class="form-group">
                    <label for="biere_description">Description</label>
                    <input v-model="biere.description" type="text" class="form-control"  aria-describedby="emailHelp" placeholder="Entrer la description">
                </div>
                <div class="form-group">
                    <label for="biere_image">Image</label>
                    <input v-model="biere.image" type="text" class="form-control"  aria-describedby="emailHelp" placeholder="Entrer l'url de l'image">
                </div>
            </form>
            <template v-slot:modal-footer="{ok }">
                <b-btn variant="secondary" @click="ok()">Cancel</b-btn>
                <b-btn variant="primary" @click="modifier(biere.id_biere), ok()" @ok ="erreur(err)">Modifier</b-btn>
            </template>
         </b-modal>
    </div>
</template>
<script>

export default {
    props:{
        err : Boolean,
        biere: Object,
        modifier : Function

    },
    methods : {
        // erreur(erreur){

        // }
    }

}
</script>