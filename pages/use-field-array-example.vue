<template>
  <div id="use-field-array-example-page">
    <category-item-select v-for="(_, i) in fields"
                          :model-name="`selectedItems[${i}]`"
                          :rules="categoryItemRules"
                          :form="form"/>
    <div class="buttons">
      <button @click="onClickAddButton">追加</button>
      <button @click="onClickSaveButton">保存</button>
      <button @click="onClickResetButton">リセット</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {useForm, useFieldArray} from 'vee-validate'
import * as yup from 'yup'

type SelectedItemType = {
  category: string,
  item: string
}

type FormType = {
  selectedItems: SelectedItemType[]
}

const categoryItemRules = {
  category: yup.string().required(),
  item: yup.string().required(),
}

const form = useForm<FormType>({
  initialValues: {
    selectedItems: [
      {
        category: '',
        item: ''
      }
    ]
  }
})

const {validate, resetForm} = form

const {fields, push} = useFieldArray<SelectedItemType>('selectedItems')

function onClickAddButton() {
  push({
    category: '',
    item: ''
  })
}

function onClickSaveButton() {
  validate()
}

function onClickResetButton() {
  resetForm({
    values: {
      selectedItems: [
        {
          category: '',
          item: ''
        }
      ]
    }
  })
}
</script>

<style lang="scss">
#use-field-array-example-page {
  .buttons {
    display: flex;
    gap: 8px;
    margin-top: 12px;

    button {
      min-width: 100px;
    }
  }
}
</style>
