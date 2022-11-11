<template>
  <div>
    <section class="topNav">
      <h2>Income Tracker</h2>
      <h3>$ {{total}}</h3>
    </section>
    <div class="container">
      <TopNav @showTotal="total=$event"></TopNav>
    </div>
  </div>
</template>

<script>
import TopNav from '../components/TopNav'
export default {
  components: { TopNav },
  data(){
    return{
      total: 0
    }
  }

}
</script>

<style>

</style>