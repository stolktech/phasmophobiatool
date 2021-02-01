<template>
  <div @click="$emit('click')"  class="ghostStatusContainer">
    <h3 class="ghostNameplate">{{ status.name }}</h3>
    <div class="tips">
    <div class="infoBtn">{{status.strength}}</div>
    <div class="infoBtn">{{status.tip}}</div>
    </div>
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
  max-width: 100vw;
  margin-bottom: .1rem;
  padding-bottom: .1rem;
  border-bottom: 1px inset rgba(0,0,0,0.1);
  display: flex;
  flex-direction: row;
  position: relative;
  text-align: left;
  &:hover {
    background-color: rgba(255,255,255,0.2);
  }
  .tips {
    flex: 1;
  }
  .ghostNameplate{
    flex: 0 0 7rem;
    margin: 0.1em;
    cursor: pointer;
  }
  .infoBtn{
    font-size: .8rem;
    margin: 0;
    margin-left: 0.5em;
    margin-right: 0.1em;
    /* border-radius: 50%; */
    width: 100%;
    cursor: pointer;
  }
}
</style>
