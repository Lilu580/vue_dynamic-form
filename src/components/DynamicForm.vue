<template>
  <div class="p-4 max-w-md mx-auto">
    <input
      v-model="searchQuery"
      placeholder="Search..."
      @input="highlightFields"
      class="mb-4 p-2 border border-gray-300 rounded w-full search-field"
      :class="{'bg-green-200': !searchMatches && searchQuery && !highlightFields()}"
    />
    <form @submit.prevent class="space-y-4">
      <div v-for="(field, index) in fields" :key="field.id" class="field-group flex items-center space-x-2">
        <input
          v-model="field.value"
          :class="{'bg-green-200': searchQuery && field.value.toLowerCase().includes(searchQuery.toLowerCase())}"
          @input="countVowels(index)"
          class="p-2 border border-gray-300 rounded flex-1"
        />
        <span>Vowels: {{ field.vowelCount }}</span>
        <button type="button" @click="removeField(index)" v-show="fields.length > 1 || index > 0" class="text-red-500">Remove</button>
      </div>
      <button type="button" @click="addField" :disabled="fields.length >= 10" class="p-2 bg-blue-500 text-white rounded">Add Field</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue';

interface Field {
  id: number;
  value: string;
  vowelCount: number;
}

export default defineComponent({
  name: 'DynamicForm',
  setup() {
    const searchQuery = ref('');
    const fields = reactive<Field[]>([
      { id: 1, value: '', vowelCount: 0 },
      { id: 2, value: '', vowelCount: 0 },
      { id: 3, value: '', vowelCount: 0 }
    ]);

    const addField = () => {
      if (fields.length < 10) {
        fields.push({
          id: fields.length + 1,
          value: '',
          vowelCount: 0
        });
      }
    };

    const removeField = (index: number) => {
      if (fields.length > 1) {
        fields.splice(index, 1);
      }
    };

    const countVowels = (index: number) => {
      const vowels = fields[index].value.match(/[aeiou]/gi);
      fields[index].vowelCount = vowels ? vowels.length : 0;
    };

    let searchMatches = ref(false);

    const highlightFields = () => {
      let matches = false;
      fields.forEach((field) => {
        if (field.value.toLowerCase().includes(searchQuery.value.toLowerCase())) {
          matches = true;
        }
      });
      return matches;
    };

    return {
      searchQuery,
      fields,
      addField,
      removeField,
      countVowels,
      highlightFields,
      searchMatches
    };
  }
});
</script>

<style scoped>
.field-group {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.field-group input {
  margin-right: 10px;
}

.field-group input.highlight {
  background-color: green;
}

button {
  margin-right: 10px;
}

input[type="text"] {
  flex: 1;
}
</style>