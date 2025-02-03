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
  <h2>## Failure Blur form</h2>
  <h3>{{ props.text }}</h3>
  <ol>
    <li>全角でテキストボックスに数字を入力 ex.１２３</li>
    <li>テキストボックスからfocusを離す。</li>
    <li>Focusが離れた後、半角数字になるので削除して同じ数字を入力する ex.１２３</li>
    <li>テキストボックスの中身の数字は全角のままになる</li>
  </ol>
  <input
    type="text"
    :value="props.text"
    :maxlength="props.maxLength"
    :minlength="props.minLength"
    @blur="(event) => handleEvent(event)"
  />
</template>
