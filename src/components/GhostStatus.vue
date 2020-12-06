<template>
  <div @click="$emit('click')"  class="ghostStatusContainer">
    <h3 class="ghostNameplate">{{ status.name }}</h3>
    <h3 @click="showGhostInfo" class="infoBtn">?</h3>
  </div>
</template>

<script>
export default {
  name: 'GhostStatus',
  props: {
    status
  },
  methods: {
    showGhostInfo(e){
      e.stopPropagation();
      this.$emit('showGhostInfo', this.status);
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.ghostStatusContainer{
  background-color: rgba(255,255,255,1);
  border: 1px inset rgba(0,0,0,0.4);
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  position: relative;
  .ghostNameplate{
    margin: 0.1em;
    cursor: pointer;
  }
  .infoBtn{
    margin: 0;
    margin-left: 0.5em;
    margin-right: 0.1em;
    border: 1px solid rgb(70,70,70);
    border-radius: 50%;
    width: 1em;
    height: 1em;
    background-color: rgb(235,235,235);
    cursor: pointer;
  }
}
</style>
