<template>
  <div>
    <!-- CAMPO PARA ADICIONAR OS NOVOS ITENS -->
    <v-text-field
      clearable
      label="Adicionar Item"
      v-model="newItem"
      @keyup.enter="addItem"
    ></v-text-field>

    <!-- CAMPO DA LISTA COM OS ITENS ADICIONADOS -->
    <v-list lines="three">
      <v-list-item
        v-for="(item, index) in items"
        :key="index"
        :title="item.title"
        :value="index"
      >
        <!-- CHECKBOX -->
        <template v-slot:prepend>
          <v-list-item-action>
            <v-checkbox-btn
              :model-value="item.checked"
              @update:model-value="(val) => updateChecked(index, val)"
            ></v-checkbox-btn>
          </v-list-item-action>
        </template>
      </v-list-item>
    </v-list>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Lista de itens com estado inicial
const items = ref([
  {
    title: "Texto qualquer",
    checked: false,
  },
]);

// Campo de entrada para novo item
const newItem = ref("");

// Adicionar um novo item à lista
const addItem = () => {
  if (newItem.value.trim() !== "") {
    items.value.push({
      title: newItem.value,
      checked: false, // Inicializa o checkbox desmarcado
    });
    newItem.value = ""; // Limpa o campo de entrada
  }
};

// Atualizar o estado do checkbox
const updateChecked = (index, value) => {
  items.value[index].checked = value;
};
</script>