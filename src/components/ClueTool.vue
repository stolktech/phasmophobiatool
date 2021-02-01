<template>
  <div class="clueToolContainer">
    <h1>Evidence</h1>
    <div class="clueOptionContainer">
      <ClueOption
        v-for="(option, optionIndex) in clues"
        v-bind:key="optionIndex"
        @click="optionSelected(option)"
        :status="option" />
    </div>
    <h1>Remaining Ghosts</h1>
    <div class="remainingGhostsContainer">
      <template
        v-for="(ghost, ghostIndex) in ghosts" >
        <GhostStatus
          v-bind:key="ghostIndex"
          @click="ghostSelected(ghost)"
          @showGhostInfo="showGhostInfo"
          v-if="ghost.remaining"
          :status="ghost"/>
      </template>
    </div>
    <div @click="resetAll()" class="resetAll">Reset</div>
    <GhostViewer v-if="ghostInfoShown" @close="ghostInfoShown = false" :ghost="currentGhostInfo" />
  </div>
</template>

<script>
import ClueOption from './ClueOption.vue'
import GhostStatus from './GhostStatus.vue'
import GhostViewer from './GhostViewer.vue'

export default {
  name: 'ClueTool',
  components: {
    ClueOption,
    GhostStatus,
    GhostViewer,
  },
  data(){
    return {
      clues: [
        {name:"EMF Lvl 5", id:'emf', found:false, eliminated:false, image: './emfreader.png'},
        {name:"Spirit Box", id:'sbox', found:false, eliminated:false, image: './spiritbox.png'},
        {name:"Fingerprints", id:'fprints', found:false, eliminated:false, image: './fingerprints.png'},
        {name:"Ghost Orb", id:'orb', found:false, eliminated:false, image: './orbs.png'},
        {name:"Ghost Writing", id:'gwriting', found:false, eliminated:false, image: './ghostwriting.png'},
        {name:"Freezing Temps", id:'ftemps', found:false, eliminated:false, image: './freezingtemps.png'},
      ],
      ghosts: [
        {name:"Demon", evidence:['sbox','ftemps','gwriting'], remaining:true, strength:"Attacks more often than any other ghost.", tip:"Asking the Demon a question on the Ouija Board wont lower sanity." },
        {name:"Banshee", evidence:['fprints','emf','ftemps'], remaining:true, strength:"Banshees focus on one target at a time and the target persists between hunts until they are killed.", tip:"Banshees are more susceptible to a crucifix."},
        {name:"Spirit", evidence:['sbox','fprints','gwriting'], remaining:true, strength:"Spirits are common but possess no special strengths.", tip:"Smudge sticks prevent a Spirit from hunting for several minutes."},
        {name:"Wraith", evidence:['sbox','fprints','ftemps'], remaining:true, strength:"Wraiths rarely touch the ground so it's tough to track by footsteps.", tip:"Salt is toxic to a Wraith."},
        {name:"Phantom", evidence:['orb','emf','ftemps'], remaining:true, strength:"Phantoms quickly drain the sanity of anyone staring at them.", tip:"Taking a photo of a Phantom will make it briefly disappear."},
        {name:"Poltergeist", evidence:['orb','sbox','fprints'], remaining:true, strength:"A poltergeist is known for throwing many objects around the room.", tip:"Empty the room of small objects to render the ghost less effective."},
        {name:"Jinn", evidence:['orb','sbox','emf'], remaining:true, strength:"A Jinn is known to close distances very rapidly with its quick speed while hunting.", tip:"Cut off the power source to slow the Jinns movement speed."},
        {name:"Mare", evidence:['orb','sbox','ftemps'], remaining:true, strength:"Mares become more hostile in the dark.", tip:"Keep lights on around the Mare and keep out of dark areas to prevent it from becoming as hostile."},
        {name:"Revenant", evidence:['fprints','emf','gwriting'], remaining:true, strength:"Revenants have increased speed while they see their victim.", tip:"Hide from a Revenant to significantly reduce its movement speed."},
        {name:"Shade", evidence:['orb','emf','gwriting'], remaining:true, strength:"Shades are very shy and wont produce much evidence if the hunters travel in groups.", tip:"A shade wont attack if you stay grouped up."},
        {name:"Yurei", evidence:['orb','ftemps','gwriting'], remaining:true, strength:"Yureis are known to have a more significant impact on hunter sanity.", tip:"Use a smudge stick in the room to prevent it from wandering for a long time."},
        {name:"Oni", evidence:['sbox','emf','gwriting'], remaining:true, strength:"An Oni becomes more active when there are more hunters nearby.", tip:"Traveling in groups makes finding evidence for an Oni far easier."},
      ],
      ghostInfoShown: false,
      currentGhostInfo: {}
    }
  },
  methods: {
    showGhostInfo(ghost){
      this.currentGhostInfo = ghost;
      this.ghostInfoShown = true;
    },
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
            const clue = this.clues.find(c => c.id === this.ghosts[i].evidence[j]);
            // this.clues[this.ghosts[i].evidence[j]].eliminated = false;
          }
        }
      }
    },

    resetAll() {
      this.ghosts.map(ghost => ghost.remaining = true);
      this.clues.map(clue => {
        clue.found = false;
        clue.eliminated = false;
      });
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
    ghostSelected(ghost) {
      this.resetAll();
      this.clues.map(clue => {
        const found = ghost.evidence.find(ev =>ev === clue.id);
        clue.found = typeof found === 'number';
        clue.eliminated =  typeof found !== 'number';
      });
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
  }
}
.resetAll {
  padding: .3rem 1rem;
  margin-top: 1rem;
  border: 1px solid black;
  cursor: pointer;
}
</style>
