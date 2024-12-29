<template>
  <div>
    <!-- CAMPO PARA ADICIONAR OS NOVOS ITENS -->
    <v-text-field clearable label="Adicionar Item" v-model="newItem" @keyup.enter="addItem"></v-text-field>

    <!-- CAMPO DA LISTA COM OS ITENS ADICIONADOS -->
    <v-list lines="two">
      <v-list-item v-for="(item, index) in items" :key="index" :title="item.title" :value="index">

        <!-- Botão de deletar item -->
        <template v-slot:append>
          <v-btn 
            color="grey-lighten" 
            icon="mdi-delete-forever" 
            variant="text"
             @click="openDeleteModal(index)"
            ></v-btn>
        </template>

      </v-list-item>
    </v-list>

    <!-- Modal -->
    <Modal :dialog="showModal"></Modal>

  </div>
</template>

<script setup>
import { ref } from 'vue';
import Modal from '@/components/Modal.vue';

// Lista de itens com estado inicial
const items = ref([
  {
    title: "Texto qualquer",
  },
]);

// Campo de entrada para novo item
const newItem = ref("");

// Adicionar um novo item à lista
const addItem = () => {
  if (newItem.value.trim() !== "") {
    items.value.push({
      title: newItem.value,
    });
    newItem.value = ""; // Limpa o campo de entrada
  }
};
// Estado do modal
const showModal =  ref(false);
// Função para abrir o modal (pode passar informações como o índice do item se necessário)
const openDeleteModal = (index) => {
  console.log(`Abrindo modal para o item: ${index}`);
  showModal.value = true;
};

</script>