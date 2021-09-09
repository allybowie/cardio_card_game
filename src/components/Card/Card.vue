<template>
  <div>
      <div class="valueRow">
        <h3>{{ cardInfo.value }}</h3>
        <h3>{{ cardInfo.face ? cardInfo.face : cardInfo.value }}</h3>
      </div>
      <h2>{{ cardInfo.exercise }}</h2>
      <div class="valueRow">
        <h3>{{ cardInfo.face ? cardInfo.face : cardInfo.value }}</h3>
        <h3>{{ cardInfo.value }}</h3>
      </div>
  </div>
</template>

<script>
export default {
  props: {
    cardInfo: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.valueRow {
  display: flex;
  justify-content: space-between;
}
</style>