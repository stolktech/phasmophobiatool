<template>
  <div @click="$emit('click')" :class="[status.found ? 'found' : 'notFound', status.eliminated ? 'eliminated': '', 'optionContainer']">
    <h4>{{ status.name }}</h4>
  </div>
</template>

<script>
export default {
  name: 'ClueOption',
  props: {
    status
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.optionContainer{
  width: 100px;
  height: 100px;
  position: relative;
  margin: 0.15em;
  border-radius: 7%;
  border: 2px inset rgba(0,0,0,0.2);
  box-shadow: 2px 3px rgba(0,0,0,0.1);
  h4 {
    position: absolute;
    bottom: 0;
    margin: 0;
    left: 0;
    right: 0;
    user-select: none;
  }
  &:hover{
    background-color: rgba(50,50,70,0.45);
    cursor: pointer;
  }
  &:active{
    background-color: rgba(50,50,70,0.5);
  }
}

.notFound {
  background-color: rgba(50,50,70,0.3);
}
.found {
  background-color: rgba(130,180,130,0.8);

  &:hover{
    background-color: rgba(90,170,90,0.8);
  }
}
.eliminated {
  background-color: rgba(240,120,120,0.8);

  &:hover{
    background-color: rgba(230,90,90,0.8);
  }
}
</style>
