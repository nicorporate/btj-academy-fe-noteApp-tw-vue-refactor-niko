<template>
    <div>
        <section id="taskCount" class="flex">
      <div
        class="flex flex-col p-2 border border-black rounded-md m-2"
        v-for="(status, index) in todoStatus"
        :key="index"
      >
        {{ status.name }}
        <div class="font-bold">{{ status.value }}</div>
      </div>
    </section>
    </div>
</template>

<script>
export default {
  inject: ['todoStatus']
}
</script>