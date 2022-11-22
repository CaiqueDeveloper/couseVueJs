<template>
  <TheHeader />
  <section class="w-full">
      <div class="container mx-auto">
          <ThePosts/>
      </div>
  </section>
  
</template>
<script>

import TheHeader from '@/components/Header/TheHeader.vue'
import ThePosts from '@/components/Posts/ThePosts.vue';

export default {
  name: 'App',
  components: {
    TheHeader,
    ThePosts
  }
}
</script>
