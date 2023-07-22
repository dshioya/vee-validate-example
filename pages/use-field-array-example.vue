<template>
  <div id="index-page">
    <category-item-select v-for="(_, i) in fields"
                          :category-name="`selectedItems[${i}].category`"
                          :item-name="`selectedItems[${i}].item`"/>
    <div class="buttons">
      <button @click="onClickAddButton">追加</button>
      <button @click="onClickSaveButton">保存</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {useForm, useFieldArray} from 'vee-validate'

type SelectedItemType = {
  category: string,
  item: string
}

type FormType = {
  selectedItems: SelectedItemType[]
}

const {values, meta, errors, validate} = useForm<FormType>({
  initialValues: {
    selectedItems: [
      {
        category: '',
        item: ''
      }
    ]
  }
})

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
</script>

<style lang="scss">
#index-page {
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
