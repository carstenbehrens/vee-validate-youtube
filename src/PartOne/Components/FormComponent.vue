<script setup>
import { useForm } from 'vee-validate'
import {string, object, ref, array} from 'yup'
import InputField from "@/PartOne/Components/InputField.vue";
import SelectionInputField from "@/PartOne/Components/SelectionInputField.vue";

const schema = object({
  name: string().required("Please enter a name"),
  email: string().email("Please enter a valid email").required("Please enter an email"),
  password: string().required("Please enter a password").min(6),
  passwordConfirm: string()
    .required("Please enter a password")
    .min(6)
    .oneOf([ref('password')], "Password must match"),
  color: array().min(1, "Please select at least one color").required("Please select a color"),
  deliveryType: string().required('Please select a delivery type')
})

const { defineInputBinds, values, errorBag, handleSubmit } = useForm({
  validationSchema: schema
})

const submit = handleSubmit(() => {
  alert(JSON.stringify(values))
})
</script>

<template>
  <form class="flex" @submit="submit">
    <input-field :define-input-binds="defineInputBinds" :error-bag="errorBag" name="name" label="Name" />
    <input-field :define-input-binds="defineInputBinds" :error-bag="errorBag" name="email" label="Email" />
    <input-field :define-input-binds="defineInputBinds" :error-bag="errorBag" name="password" label="Password" input-type="password" />
    <input-field :define-input-binds="defineInputBinds" :error-bag="errorBag" name="passwordConfirm" input-type="password" />
    <selection-input-field :values="['red', 'green', 'blue']" :error-bag="errorBag" name="color" label="Colors" />
    <selection-input-field :values="['Slow', 'Fast', 'Super Fast']" :error-bag="errorBag" name="deliveryType" input-type="radio" label="Delivery Type" />
    <button type="submit">
      Submit
    </button>
  </form>
</template>

<style scoped>
.flex {
  max-width: 20rem;
  display: flex;
  flex-direction: column;
}
</style>
