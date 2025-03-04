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

// inputかつ、inputの入力が終了している場合にeventを発火
// inputでイベントを常時発行していると、inputをはみ出して入力ができてしまう。
const handleInput = (event: Event) => {
  const { target } = event

  if (!(event instanceof InputEvent)) {
    return
  }
  if (event.isComposing) {
    return
  }
  if (!(target instanceof HTMLInputElement)) {
    return
  }
  emits('first-half-input', target.value)
}

const finishComposition = (event: Event) => {
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
    <li>
      inputで常にイベントが発火するようにするが、compositionendが確定していない状態のときはinputイベントを発行しないようにする
    </li>
    <li>
      inputとcompositionの状態で検知しているので、一度数字を消して違う数字を入れてもイベントが発火する
    </li>
  </ul>
  <input
    type="text"
    :value="props.text"
    :maxlength="props.maxLength"
    :minlength="props.minLength"
    @input="(event) => handleInput(event)"
    @compositionend="(event) => finishComposition(event)"
  />
</template>
