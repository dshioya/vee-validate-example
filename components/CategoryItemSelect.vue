<template>
  <div class="category-item-select-ct">
    <div class="category-field">
      <select v-model="categoryValue">
        <option v-for="option in categoryOptions"
                :value="option.value">{{ option.label }}
        </option>
      </select>
      <div v-if="categoryErrorMessage" class="field-error">{{ categoryErrorMessage }}</div>
    </div>
    <div class="item-field">
      <select v-model="itemValue">
        <option v-for="option in itemOptions"
                :value="option.value">{{ option.label }}
        </option>
      </select>
      <div v-if="itemErrorMessage" class="field-error">{{ itemErrorMessage }}</div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {defineProps, PropType} from 'vue'
import {useField, FormContext, useForm} from 'vee-validate'

const props = defineProps({
  modelName: {
    type: String,
    required: true
  },
  rules: {
    type: Object,
    required: true
  },
  form: {
    type: Object as PropType<FormContext>,
    required: true
  }
})

const {
  value: categoryValue,
  errorMessage: categoryErrorMessage
} = useField(`${props.modelName}.category`, props.rules.category, {form: props.form})

const {
  value: itemValue,
  errorMessage: itemErrorMessage
} = useField(`${props.modelName}.item`, props.rules.item, {form: props.form})

const categoryOptions = [
  {
    label: '',
    value: ''
  },
  ...[1, 2, 3].map(i => ({
    label: `カテゴリ${i}`,
    value: `category${i}`
  }))
]

const itemOptions = [
  {
    label: '',
    value: ''
  },
  ...[1, 2, 3, 4, 5].map(i => ({
    label: `項目${i}`,
    value: `item${i}`
  }))
]
</script>

<style lang="scss">
.category-item-select-ct {
  display: flex;
  gap: 8px;
  margin-bottom: 12px;

  select {
    padding: 12px;
  }

  .field-error {
    color: #dc2626;
    font-size: 11px;
  }
}
</style>
