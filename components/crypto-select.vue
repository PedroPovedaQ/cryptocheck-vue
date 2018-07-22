<template lang="html">
  <div class="crypto-container">
    <sui-dropdown
    icon="world"
    placeholder="Select Currency"
    selection
    :options="options"
    v-model="current"
  />
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: null,
      options: [{
        text: 'Bitcoin',
        value: 1,
      }, {
        text: 'Litecoin',
        value: 2,
      }],
    };
  },
  methods: {
  },
  watch: {
    current(){
      console.log('current has changed!');
    }
  }
}
</script>

<style>
.crypto-container {
  text-align: center;
  margin-top: 5vh;
}
</style>
