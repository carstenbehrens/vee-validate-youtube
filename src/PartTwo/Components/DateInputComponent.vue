<template>
  <label-component text="Date" />
  <VueDatePicker
    v-model="value"
    @blur="validate"
  />
  <error-message :message="errorMessage" />
</template>
<script setup>
import LabelComponent from "@/PartTwo/Components/LabelComponent.vue";
import ErrorMessage from "@/PartTwo/Components/ErrorMessage.vue";
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'
import { useField } from "vee-validate";
import {string} from "yup";

const { value, validate, errorMessage } = useField('date',
  string().required("Please enter a date"))

</script>