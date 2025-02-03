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
const isCompositionActive = ref(false)

// inputかつ、inputの入力が終了している場合にeventを発火
// inputでイベントを常時発行していると、inputをはみ出して入力ができてしまう。
const handleInput = (event: Event) => {
  const { target } = event

  if (!(target instanceof HTMLInputElement)) {
    return
  }
  if (isCompositionActive.value) {
    return
  }
  emits('first-half-input', target.value)
}

const activateIsComposition = () => {
  isCompositionActive.value = true
}

//IMEの入力の終了フラグを立てて親コンポーネントにイベント発火
const finishComposition = (event: Event) => {
  isCompositionActive.value = false

  const { target } = event
  if (!(target instanceof HTMLInputElement)) {
    return
  }
  emits('first-half-input', target.value)
}
</script>

<template>
  <h2># success form</h2>
  <h3>{{ props.text }}</h3>
  <ul>
    <li>compositionendでIMEの確定を検知する</li>
    <li>inputで常にイベントが発火するようにするが、compositionendが確定していない状態のときはinputイベントを発行しないようにする</li>
    <li>inputとcompositionの状態で検知しているので、一度数字を消して違う数字を入れてもイベントが発火する</li>
  </ul>
  <input
    type="text"
    :value="props.text"
    :maxlength="props.maxLength"
    :minlength="props.minLength"
    @input="(event) => handleInput(event)"
    @compositionstart="activateIsComposition()"
    @compositionend="(event) => finishComposition(event)"
  />
</template>
