<template>
<CounterVue :year="2024" :month="8" :date="24" :hour="23" :minute="55" :second="59" :millisecond="31"></CounterVue>
</template>
<script >
import CounterVue from './components/Counter.vue'
export default {
 components: {
  CounterVue
 }
}
</script>
<style scoped>

</style>
