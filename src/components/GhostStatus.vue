<template>
  <div @click="$emit('click')"  class="ghostStatusContainer">
    <h3>{{ status.name }}</h3>
  </div>
</template>

<script>
export default {
  name: 'GhostStatus',
  props: {
    status
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.ghostStatusContainer{
  background-color: rgba(255,255,255,1);
  border: 1px inset rgba(0,0,0,0.4);
  h3{
    margin: 0.1em;
    text-align: left;
    cursor: pointer;
  }
}
</style>
