<template>
  <a-progress
  type="circle"
  :stroke-color="{
    '0%': '#108ee9',
    '100%': '#87d068',
  }"
  :format="percent => `${this.value} ${label}`"
  status="normal"
  :percent="countPercentage()"
  />
</template>

<script>
export default {
  name: 'Speedometer',
  props: {
    label: { default: 'MB/s' },
    value: { required: true },
    max: { default: 100 }
  },
  data () {
    return {

    }
  },
  methods: {
    countPercentage () {
      return Math.floor(this.value / this.max * 100)
    }
  }
}
</script>

<style></style>