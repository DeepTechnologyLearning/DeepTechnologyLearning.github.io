<template>
  <div class="home">
    <Section_1 />
    <Section_2 />
    <Section_3 />
    <Section_4 />
    <Section_5 />
    <Section_6 />
    <Section_7 />
  </div>
</template>

<script>
// @ is an alias to /src
import Section_1 from '@/components/home/Section_1.vue'
import Section_2 from '@/components/home/Section_2.vue'
import Section_3 from '@/components/home/Section_3.vue'
import Section_4 from '@/components/home/Section_4.vue'
import Section_5 from '@/components/home/Section_5.vue'
import Section_6 from '@/components/home/Section_6.vue'
import Section_7 from '@/components/home/Section_7.vue'

export default {
  name: 'HomeView',
  components: {
    Section_1,
    Section_2,
    Section_3,
    Section_4,
    Section_5,
    Section_6,
    Section_7
  }
}
</script>

<style scoped>
.home {
  min-height: 100vh;
}
</style>
