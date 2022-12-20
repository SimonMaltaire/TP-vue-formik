<template>
  <form @onSubmit.prevent="state.handleSubmit">
    <slot
      :values="initialValues" 
      :errors="state.errors" 
      :handleSubmit="state.handleSubmit" 
      :isSubmitting="state.isSubmitting">
    </slot>
  </form>
</template>


<script setup>
/* eslint-disable */
import { provide, reactive, defineProps, defineEmits } from 'vue';

defineProps({
  initialValues: {
    type: Object,
    default() {
      return { name: '', email: '', password: ''}
    },
  },
  validate: {
    type: Function,
    default: null,
  },
});


const emit = defineEmits(["onSubmit"]);

const state = reactive({
values: {},
errors: {},
isSubmitting: false,

addValue: (name, value = "") => {
  state.values[name] = value;
},

updateValue: (name, value) => {
  state.values[name] = value;
},

handleSubmit: async (e) => {
  state.isSubmitting = true;
  state.errors = await validate(state.values);
  
  if (Object.keys(state.errors).length === 0) {
    emit('onSubmit', state.values);
  }
  state.isSubmitting = false;
}
});

provide('form-data', state);
</script>

