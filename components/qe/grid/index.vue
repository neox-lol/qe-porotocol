<script setup lang="ts">
interface Props {
  modelValue: string;
  foo?: string;
}
let { modelValue, foo = "default-val" } = defineProps<Props>();
const emit = defineEmits(["update:modelValue"]);
</script>
<template>
  <div w-100vh h-100vh grid grid-cols-10 gap-1 bg-red>
    <div v-for="i in 100" bg-blue>
      {{ i }}
    </div>
  </div>
</template>
