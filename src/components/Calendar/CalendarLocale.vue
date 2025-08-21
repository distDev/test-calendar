<template>
  <div class="calendar-locale">
    <button
      v-for="locale in localeList"
      :key="locale"
      class="locale-toggle"
      :class="{ active: locale === selectedLocale }"
      @click="toggleLocale(locale)"
    >
      {{ locale.toUpperCase() }}
    </button>
  </div>
</template>

<script lang="ts">
export default { name: 'CalendarLocale' }
</script>

<script setup lang="ts">
import { ref } from 'vue'

const emits = defineEmits(['update:modelValue'])

const selectedLocale = ref('ru')
const localeList = ['ru', 'en']

const toggleLocale = (locale: string) => {
  selectedLocale.value = locale
  emits('update:modelValue', locale)
}
</script>

<style scoped>
.calendar-locale {
  display: flex;
  margin-top: 20px;
}

.locale-toggle {
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

.active {
  background: #007bff;
  color: #ffffffff;
}
</style>
