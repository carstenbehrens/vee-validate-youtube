<script setup>
import {useForm} from "vee-validate";
import InputComponent from "@/PartTwo/Components/InputComponent.vue";
import PasswordInputComponent from "@/PartTwo/Components/PasswordInputComponent.vue";
import SelectionComponent from "@/PartTwo/Components/SelectionComponent.vue";
import {array, string} from "yup";
import DateInputComponent from "@/PartTwo/Components/DateInputComponent.vue";

const { handleSubmit } = useForm()

const submit = handleSubmit((values) => {
  alert(JSON.stringify(values))
})
</script>

<template>
  <form class="flex flex-col bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit="submit">
    <input-component
      :schema="string().required('Please enter a name')"
      name="name"
      label="Name"
    />
    <input-component
      :schema="string().email('Please enter a valid email').required('Please enter a email')"
      name="email"
      label="Email"
    />
    <password-input-component />
    <selection-component
      label="Colors"
      :values="['red', 'green', 'blue']"
      :schema="array()
        .min(1, 'Please select at least one color')
        .required('Please select a color')" name="color" />
    <selection-component
      label="Delivery Type"
      :values="['Slow', 'Fast', 'Super Fast']"
      input-type="radio"
      :schema="string().required('Please select a delivery type')" name="deliveryType" />
    <date-input-component />
    <button
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline mt-2"
      type="submit">Submit</button>
  </form>
</template>