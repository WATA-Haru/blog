<script setup lang="ts">
import inputIMESuccess from '@/components/inputIMESuccess/Container.vue'

import inputIMEFailureBlur from '@/components/inputIMEFailureBlur/Container.vue'
import inputIMEFailureComposition from '@/components/inputIMEFailureComposition/Container.vue'
import inputIMEFailureEnter from '@/components/inputIMEFailureEnter/Container.vue'
import inputIMEFailureInput from '@/components/inputIMEFailureInput/Container.vue'
import inputIMEFailureChange from '@/components/inputIMEFailureChange/Container.vue'
</script>

<template>
  <h1>Success</h1>
  <inputIMESuccess />
  <h1>Failure</h1>
  <inputIMEFailureBlur />
  <inputIMEFailureComposition />
  <inputIMEFailureEnter />
  <inputIMEFailureInput />
  <inputIMEFailureChange />
</template>
