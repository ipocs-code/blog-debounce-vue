<template>
<input
    type="text"
    name="fullName"
    placeholder="Enter your full name"
    v-model="myName"
    :disabled="submitted"
/>
<pre>Input is: {{ myName }}</pre>

<button type="button"
    @click="handleSubmit"
    :disabled="!myName || submitted"
>
    <span v-if="!submitted">SUBMIT NAME</span>
    <span v-else>Loading...</span>
</button>
</template>

<script setup>
import { ref } from 'vue'
import {
    useDebounce,
    useDebounceFn
} from './composables/useDebounce'

const myName = useDebounce('', 600)
const submitted = ref(false)

const myDebouncedMethod = useDebounceFn(() => {
    // just reset the myName and submitted values for testing
    myName.value = ''
    submitted.value = false
}, 2000)

const handleSubmit = () => {
    submitted.value = true
    myDebouncedMethod()
}
</script>
