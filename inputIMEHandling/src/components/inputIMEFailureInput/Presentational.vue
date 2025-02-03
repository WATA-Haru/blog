<script setup lang="ts">
import { ref } from 'vue'

interface Props {
  text: string
  minLength: number
  maxLength: number
}

interface Emits {
  (event: 'first-half-input', text: string): void
}

const props = defineProps<Props>()
const emits = defineEmits<Emits>()

const handleEvent = (event: Event) => {
  const { target } = event

  if (!(target instanceof HTMLInputElement)) {
    return
  }
  emits('first-half-input', target.value)
}
</script>

<template>
  <h2>## Failure Input form</h2>
  <h3>{{ props.text }}</h3>
  <p>全角数字をずっと押し続けるとmaxlengthプロパティを無視して入力ができる</p>
  <input
    type="text"
    :value="props.text"
    :maxlength="props.maxLength"
    :minlength="props.minLength"
    @input="(event) => handleEvent(event)"
  />
</template>
