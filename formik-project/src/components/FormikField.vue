<template>
    <input :name="name" :type="type">
</template>

<script setup>
import { defineProps } from "vue";
defineProps({
    type: {
        type: String,
        required: false,
        default: 'text'
    },
    name: {
        type: String,
        required: true,
    }
});
</script>