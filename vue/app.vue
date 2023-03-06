<template>
  <div class="wrapper-st">

      <a-row>
        <a-col :span="12">
          <b>Download speed</b>
          <p>{{ uploadSpeedAvg }} MB/s</p>
          <speedometer class="speedometer" :value="downloadSpeed" max="100"></speedometer>
        </a-col>
        <a-col :span="12">
          <b>Upload speed</b>
          <p>{{ downloadSpeedAvg }} MB/s</p>
          <speedometer :value="uploadSpeed" max="100"></speedometer>
        </a-col>
      </a-row>

      <a-divider/>

        <a-button v-if="!running" @click="doTest" class="space" type="primary">Start test</a-button>
        <a-button v-if="running" class="space" type="primary" disabled>Start test</a-button>

        <br/>
        <a-space class="space">
          <a-select ref="select" v-model="action" style="width: 120px">
            <a-select-option v-for="(action, key) in actions" :key="key">{{ action }}</a-select-option>
          </a-select>
        </a-space>
        <br/>
        <a-textarea placeholder="Console log" :rows="4" disabled/>
  </div>
</template>

<script>
import Speedometer from './Speedometer.vue'

const Action = {
  AUTO: 0,
  DOWNLOAD: 1,
  UPLOAD: 2,
  GET_LOCATION: 3
}

export default {
  components: { Speedometer },
  data () {
    return {
      running: false,

      uploadSpeed: 0,
      uploadSpeedAvg: 0,
      downloadSpeed: 0,
      downloadSpeedAvg: 0,

      action: Action.AUTO,
      actions: [
        'Auto',
        'Download',
        'Upload',
        'Get location'
      ]
    }
  },
  methods: {
    doTest () {
      this.$rpc.call('libspeedtest', 'test', {}).then(r => {
        console.log(r)
      })
    }
  }
}
</script>

<style>
.wrapper-st {
  width: 500px;
  text-align: center;
  justifyContent: 'center';
}
.speedometer {
  margin-right: 15px;
}

.space {
  margin-bottom: 10px;
}
</style>
