<template>
  <TheHeader />

  <section class="w-full">
      <div class="container mx-auto">
          <TodosComponent/>
      </div>
  </section>
</template>
<script>

import TheHeader from '@/components/Header/TheHeader.vue'
import TodosComponent from '@/components/Todos/TheTodosList.vue';
export default {
  name: 'App',
  components: {
    TheHeader,
    TodosComponent
  }
}
</script>
