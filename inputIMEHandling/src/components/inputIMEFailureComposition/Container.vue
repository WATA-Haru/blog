<script setup lang="ts">
import { convertStringNumToNaturalNum } from '@/utils/convertStringNumToNaturalNum'
import { isStringNaturalNum } from '@/utils/isStringNaturalNum'
import { ref } from 'vue'
import Presentational from './Presentational.vue'

defineOptions({
  name: 'inputIMEFailureComposition',
})

const textRef = ref('')

const handleFirstHalfInput = (textFromInput: string) => {
  // textFromInputが数字以外を含む場合にエラーを返す
  if (!isStringNaturalNum(textFromInput)) {
    console.error(`invalid INPUT ${textFromInput}`)
  }

  // textFromInputが全角の場合に、半角にconvertしてvalueに結合
  let s = ''
  for (const c of textFromInput) {
    s += String(convertStringNumToNaturalNum(c))
  }
  textRef.value = s
}
</script>
<template>
  <Presentational
    :text="textRef"
    @first-half-input="handleFirstHalfInput"
    :min-length="3"
    :max-length="3"
  />
</template>
