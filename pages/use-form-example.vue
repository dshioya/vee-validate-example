<template>
  <div id="use-form-example-page">
    <div>
      <input type="text" v-bind="name" />
      <div v-if="errors.name">{{ errors.name }}</div>
    </div>
    <div>
      <input type="text" v-bind="email" />
      <div v-if="errors.email">{{ errors.email }}</div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {useForm} from 'vee-validate'
import * as yup from 'yup'

const {values, errors, validate, defineInputBinds} = useForm({
  initialValues: {
    name: '',
    email: ''
  },
  validationSchema: yup.object({
    name: yup.string().required(),
    email: yup.string().required(),
  })
})

const name = defineInputBinds('name')
const email = defineInputBinds('email')
</script>

<style lang="scss">
#use-form-example-page {

}
</style>
