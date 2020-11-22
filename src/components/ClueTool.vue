<template>
  <div class="clueToolContainer">
    <h1>Evidence</h1>
    <div class="clueOptionContainer">
      <ClueOption v-for="(option, optionIndex) in clues" @click="optionSelected(option)" :status="option" />
    </div>
    <h1>Remaining Ghosts</h1>
    <div class="remainingGhostsContainer">
      <GhostStatus v-for="(ghost, ghostIndex) in ghosts" v-if="ghost.remaining" :status="ghost"/>
    </div>
  </div>
</template>

<script>
import ClueOption from './ClueOption.vue'
import GhostStatus from './GhostStatus.vue'
export default {
  name: 'ClueTool',
  components: {
    ClueOption,
    GhostStatus
  },
  data(){
    return {
      clues: [
        {name:"Ghost Orb", id:0, found:false, eliminated:false},
        {name:"Spirit Box", id:1, found:false, eliminated:false},
        {name:"Fingerprints", id:2, found:false, eliminated:false},
        {name:"EMF Lvl 5", id:3, found:false, eliminated:false},
        {name:"Freezing Temps", id:4, found:false, eliminated:false},
        {name:"Ghost Writing", id:5, found:false, eliminated:false},
      ],
      ghosts: [
        {name:"Demon", evidence:[1,4,5], remaining:true},
        {name:"Banshee", evidence:[2,3,4], remaining:true},
        {name:"Spirit", evidence:[1,2,5], remaining:true},
        {name:"Wraith", evidence:[1,2,4], remaining:true},
        {name:"Phantom", evidence:[0,3,4], remaining:true},
        {name:"Poltergeist", evidence:[0,1,2], remaining:true},
        {name:"Jinn", evidence:[0,1,3], remaining:true},
        {name:"Mare", evidence:[0,1,4], remaining:true},
        {name:"Revenant", evidence:[2,3,5], remaining:true},
        {name:"Shade", evidence:[0,3,5], remaining:true},
        {name:"Yurei", evidence:[0,4,5], remaining:true},
        {name:"Oni", evidence:[1,3,5], remaining:true},
      ],
    }
  },
  methods: {
    updateGhosts(){
      for(let i = 0; i < this.ghosts.length; i++){
        let evidence = this.ghosts[i].evidence;
        this.ghosts[i].remaining = true;
        for(let j = 0; j < this.clues.length; j++){
          if(this.clues[j].found && !evidence.includes(this.clues[j].id)){
            this.ghosts[i].remaining = false;
          }
        }
      }
    },
    updateClues(){
      for(let i = 0; i < this.clues.length; i++){
        this.clues[i].eliminated = true;
      }
      for(let i = 0; i < this.ghosts.length; i++){
        if(this.ghosts[i].remaining){
          for(let j = 0; j < this.ghosts[i].evidence.length; j++){
            console.log(this.ghosts[i].evidence[j])
            this.clues[this.ghosts[i].evidence[j]].eliminated = false;
          }
        }
      }
    },
    updateStatus(){
      this.updateGhosts();
      this.updateClues();
    },
    optionSelected(clueOption){
      if(!clueOption.eliminated){
        clueOption.found = !clueOption.found
        this.updateStatus();
      }
    },

  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.clueOptionContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
.clueToolContainer {
  display: flex;
  flex-direction: column;
  align-items: center;
  h1 {
    margin:0;
    margin-bottom: 0.3em;
    margin-top: 0.3em;
    user-select: none;
  }
}
</style>
