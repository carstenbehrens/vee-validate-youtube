<template>
  <div class="flex">
    <label v-if="label">{{ label }}</label>
    <div>
      <div v-for="(value, i) of values"
      :key="i"
      >
        <Field :name="name" :type="inputType" :value="value" />
        {{ value }}
      </div>
    </div>
    <div
      v-if="getError(name)"
      class="error"
    >
      {{ getError(name) }}
    </div>
  </div>
</template>

<script setup>
import { Field } from 'vee-validate'
import {toRef} from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  label: {
    type: [String, Boolean],
    default: false,
    required: false
  },
  errorBag: {
    type: Object,
    required: true
  },
  inputType: {
    type: String,
    default: 'checkbox',
    required: false
  },
  values: {
    type: Array,
    required: true
  }
})

const errorBag = toRef(props, 'errorBag')

const getError = (name) => {
  const err = errorBag.value[name]
  return err ? err[0] : false
}


</script>

<style scoped>
label {
  margin-top: 1rem;
}

.flex {
  max-width: 20rem;
  display: flex;
  flex-direction: column;
}

.error {
  color: red;
}
</style>