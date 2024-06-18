<template>
  <div>
    <input
      v-model="searchQuery"
      placeholder="Search..."
      @input="highlightFields"
    />
    <form @submit.prevent>
      <div v-for="(field, index) in fields" :key="field.id" class="field-group">
        <input
          v-model="field.value"
          :class="{ highlight: searchQuery && field.value.includes(searchQuery) }"
          @input="countVowels(index)"
        />
        <span>Vowels: {{ field.vowelCount }}</span>
        <button type="button" @click="removeField(index)" v-if="fields.length > 1">Remove</button>
      </div>
      <button type="button" @click="addField" :disabled="fields.length >= 10">Add Field</button>
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
      { id: 1, value: '', vowelCount: 0 }
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

    const highlightFields = () => {
      fields.forEach((field, index) => {
        countVowels(index);
      });
    };

    return {
      searchQuery,
      fields,
      addField,
      removeField,
      countVowels,
      highlightFields
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