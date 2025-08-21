<template>
  <div class="calendar-nav">
    <button @click="$emit('prev-month')">‹</button>

    <span>{{ currentMonth }}</span>

    <button @click="$emit('next-month')">›</button>
  </div>
</template>

<script lang="ts">
export default { name: 'CalendarNav' }
</script>

<script setup lang="ts">
import { computed } from 'vue'
import { Dayjs } from 'dayjs'

const props = defineProps<{
  currentDate: Dayjs
  locale: string
}>()

const currentMonth = computed(() => {
  return props.currentDate.locale(props.locale).format('MMMM YYYY')
})
</script>

<style scoped>
.calendar-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
  font-weight: bold;

  button {
    border: none;
    background: #e2eaf8;
    padding: 5px 15px;
    border-radius: 6px;

    &:hover {
      opacity: 90%;
      cursor: pointer;
    }
  }
}
</style>
