<template>
  <div class="wrapper" id="wrapper" @mousedown="setMouseDown($event)" @mouseup="setMouseUp()" @mousemove="dragBackground($event); dragBackgroundCard($event);">
    <div id="holder_drag" :style="{'transform':'translate('+holder.pos_x+'px,'+holder.pos_y+'px)'}">
      <CardTile v-for="(item, index) in cards" :key="item" :transform="item" @mousedown="setMouseDownCard($event, index)" @mouseup="setMouseUpCard($event)" :style="{'z-index':item.z_index}"/>
    </div>
  </div>
</template>

<script>
import CardTile from './components/CardTiles.vue'

export default {
  name: 'App',
  components: {
    CardTile
  },
  data: function(){
    return {
      mouse_down:false,
      is_card_blocker:false,
      top_z_index:1,
      mouse_positions:{
        start_x:0,
        start_y:0
      },
      holder:{
        pos_x:100,
        pos_y:100
      },
      cards:[
        {
          pos_x:0, 
          pos_y:0,
          z_index:0
        },
        {
          pos_x:400, 
          pos_y:0,
          z_index:0
        }
      ]
    }
  },
  methods:{
    setMouseDown: function(e){
      document.getElementById("wrapper").style.cursor = "grabbing";
      this.mouse_down = true;

      //GET THE START POSITION OF THE MOUSE SO WE CAN OFFSET WHEN MOVE
      this.mouse_positions.start_x = e.clientX;
      this.mouse_positions.start_y = e.clientY;
    },
    setMouseUp: function(){
      document.getElementById("wrapper").style.cursor = "default";
      this.mouse_down = false;
      this.is_card_blocker = false;
    },
    dragBackground: function(e){
      if(this.mouse_down && !this.is_card_blocker){
        //CALCULATE HOW MUCH OUR MOUSE MOVED TO OFFSET THE HOLDER
        this.holder.pos_x += e.clientX - this.mouse_positions.start_x;
        this.holder.pos_y += e.clientY - this.mouse_positions.start_y;

        //RESET THE START POSITIONS TO THE NEW MOUSE POSITION
        this.mouse_positions.start_x = e.clientX;
        this.mouse_positions.start_y = e.clientY;
      }
    },


    // THIS IS REDUNDANT TO THE ABOVE CODE BUT DON'T HAVE ANYTHING BETTER YET
    setMouseDownCard: function(e, index){
      document.getElementById("wrapper").style.cursor = "grabbing";
      this.index = index;
      this.is_card_blocker = true;

      // GET THE START POSITION OF THE MOUSE SO WE CAN OFFSET WHEN MOVE
      this.mouse_positions.start_x = e.clientX;
      this.mouse_positions.start_y = e.clientY;


      // PUT THIS CARD ON TOP
      this.top_z_index += 1;
      this.cards[this.index]['z_index'] = this.top_z_index;
    },
    setMouseUpCard: function(){
      this.is_card_blocker = false;
      document.getElementById("wrapper").style.cursor = "default";
      this.mouse_down = false;
      this.is_card_blocker = false;
      this.index = null;
    },
    dragBackgroundCard: function(e){
      if(this.is_card_blocker && this.index != null){
        //CALCULATE HOW MUCH OUR MOUSE MOVED TO OFFSET THE HOLDER
        this.cards[this.index].pos_x += e.clientX - this.mouse_positions.start_x;
        this.cards[this.index].pos_y += e.clientY - this.mouse_positions.start_y;

        //RESET THE START POSITIONS TO THE NEW MOUSE POSITION
        this.mouse_positions.start_x = e.clientX;
        this.mouse_positions.start_y = e.clientY;
      }
    },
  },
  mounted() {
    //this.dragBackground()
  }
}
</script>

<style>
@import 'bootstrap/dist/css/bootstrap.min.css';

.wrapper{
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-color: #324365;
}

#holder_drag{
  width: 100vw;
  height: 100vh;
  transform: translate(100px, 105px);
}
</style>
