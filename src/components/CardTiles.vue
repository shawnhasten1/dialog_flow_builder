<template>
  <div class="node-card p-2" @click="alert('TEST')" :style="{'transform':'translate('+transform.pos_x+'px,'+transform.pos_y+'px)'}">
      <div class="node-card-title">
        <div class="row">
            <div class="col-3 node-mover">
                      <img src="../assets/img/trash.png" width="20">
            </div>
            <div class="col-6 node-text">Test Title</div>
            <div class="col-3 node-anchor">
                <img src="../assets/img/edit.png" width="22">
            </div>
        </div>
      </div>
      <div class="node-card-body">
          <div class="node-card-tile">
              <div class="row">
                  <div class="col-3 node-mover">
                      <img src="../assets/img/3-bar.png" width="25">
                  </div>
                  <div class="col-6 node-text">Type</div>
                  <div class="col-3 node-anchor">
                      <img src="../assets/img/anchor.png" width="15">
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'CardTile',
  props: {
      transform:Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .node-card{
        width: 300px;
        height: auto;
        border-radius: 5px;
        border: 1px solid #212d46;
        background: #293855;
        -webkit-touch-callout: none; /* iOS Safari */
        -webkit-user-select: none; /* Safari */
        -khtml-user-select: none; /* Konqueror HTML */
        -moz-user-select: none; /* Old versions of Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
        user-select: none; /* Non-prefixed version, currently
                                supported by Chrome, Edge, Opera and Firefox */
        position: absolute;
    }
    .node-card-title{
        color: white;
        text-align: center;
    }
    .node-card-body{
        margin-top: 15px;
    }
    .node-card-tile{
        color: white;
        text-align: center;
        padding-left: 1.2em;
        padding-right: 1.2em;
        padding-top: .6em;
        padding-bottom: .6em;
        background: #324365;
        border: 1px solid #212d46;
        border-radius: 5px;
        margin-top: 5px;
        margin-bottom: 5px;
    }
    .node-mover{
        text-align: left;
        transition: .8s;
    }
    .node-mover:hover{
        cursor: pointer;
        opacity: .8;
    }
    .node-anchor{
        text-align: right;
        transition: .8s;
    }
    .node-anchor:hover{
        cursor: crosshair;
        opacity: .8;
    }
</style>