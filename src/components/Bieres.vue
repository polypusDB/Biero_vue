<template>
    <div v-if = "biere != undefined">
        <b-jumbotron>
            <template v-slot:lead>
                {{biere.nom}}
            </template>
            <hr class="my-4">
            <p>Brasserie : {{biere.brasserie}}</p>
            <b-button @click = "formModifier(biere)" variant="primary" v-b-modal.modal-modifier>Modifier</b-button>
            <!-- <b-button @click = "effacer(biere.id_biere)" variant="success" href="#" >Supprimer</b-button> -->
            <b-button @click = "effacer(biere)" v-b-modal.modal-sup variant="danger">Supprimer</b-button>
            
        </b-jumbotron>
    </div>
</template>

<script>

export default {
    props:{
        biere: Object,
        effacer: Function,
        modifier: Function,
        formModifier: Function,
    },
    mounted(){
    }
}
</script>