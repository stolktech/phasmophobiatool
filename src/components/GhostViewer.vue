<template>
  <div class="viewerContainer">
    <div class="bg" @click="$emit('close')"></div>
    <div class="viewerContentBox">
      <span class="exitBtn" @click="$emit('close')">X</span>
      <h1>{{ghost.name}}</h1>

      <h3>Strengths</h3>
      <p>{{ghost.strength}}</p>

      <h3>Tip</h3>
      <p>{{ghost.tip}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GhostViewer',
  props: ['ghost'],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.viewerContainer {
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  .bg{
    position: absolute;
    width: 100%;
    height: 100%;
    left:0;
    top:0;
    background-color: rgba(0,0,0,0.8);
  }
  .viewerContentBox{
    position: relative;
    width: 50em;
    height: 40em;
    max-width: 80vw;
    max-height: 80vh;
    background-color: rgb(255,255,255);
    border-radius: 0.6%;
    box-shadow: 4px 5px rgba(0,0,0,0.3);
    h3 {
      text-align: left;
      margin-left: 2%;
    }
    p {
      text-align: left;
      margin-left: 4%;
      margin-right: 4%;
      background-color: rgba(0,0,0,0.1);
      padding: 0.2em;
    }
    .exitBtn{
      position: absolute;
      right: 0.5em;
      top: 0.5em;
      background-color: rgb(235,235,235);
      width: 1.5em;
      height: 1.5em;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: bold;
      border: 1px solid rgb(70,70,70);
      cursor: pointer;
    }
  }
}
</style>
