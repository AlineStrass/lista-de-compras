<template>
    <div class="text-center pa-4">
        <v-dialog 
            v-model="localDialog" 
            max-width="400" 
            persistent
            >
            <v-card prepend-icon="mdi-map-marker" 
                text="Tem Certeza que deseja excluir?"
                title="Tem Certeza que deseja excluir?"
                >
                <template v-slot:actions>
                    <v-spacer></v-spacer>

                    <v-btn @click="localDialog = false">
                        Cancelar
                    </v-btn>

                    <v-btn @click="localDialog = false">
                        Excluir
                    </v-btn>
                </template>
            </v-card>
        </v-dialog>
    </div>
</template>

<script setup>
import { defineProps, ref, watch } from 'vue';

// Define as props recebidas do componente pai
const props = defineProps({
    dialog: Boolean,
});

// Evento emitido para o componente pai
const emit = defineEmits(["update:dialog"]);

// Define uma versão local da prop `dialog`
const localDialog = ref(props.dialog);

// Sincroniza a prop `dialog` com a versão local
watch(
    () => props.dialog,
    (newValue) => {
        localDialog.value = newValue;
    }
);

// Emite eventos para o componente pai quando o valor local muda
watch(
    () => localDialog.value,
    (newValue) => {
        emit('update:dialog', newValue);
    }
);

// Ação de confirmação
const confirmAction = () => {
  console.log("Item excluído!");
  localDialog.value = false; // Fechar o modal
};

</script>