<template>
        <div>
        
        <b-modal id="modal-sup" centered title="BootstrapVue" i.e. ok-only>
            <p>Êtes-vous certain de vouloir supprimer</p>

            <template v-slot:modal-footer="{ok }">
                <b-btn variant="primary" @click="effacer(), ok()" >Supprimer</b-btn>
                <b-btn variant="secondary" @click="ok()">Cancel</b-btn>
            </template>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        effacer : Function
    }
}
</script>