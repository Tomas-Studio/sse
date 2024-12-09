<script lang="ts" setup>
const eventSource = ref<EventSource>()
const data = ref()

const init = () => {
  eventSource.value = new EventSource('/api/sse')
  eventSource.value.onmessage = (e) => {
    data.value = e.data
  }
}

onMounted(init)

onBeforeUnmount(() => {
  eventSource.value?.close()
})
</script>

<template>
  <div>
    {{ data }}
  </div>
</template>

