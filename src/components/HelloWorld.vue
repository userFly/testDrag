<template>
  <div>
    <div class="text">
      <div v-for="item in layout" :key="item.i">
        <input v-model="item.x">
        <input v-model="item.y">
        <input v-model="item.w">
        <input v-model="item.h">
        <input v-model="item.i">
        <button @click="deleteLayout(item.i)">删除</button>
        <button @click="updateLayout(item.i)">修改</button>
      </div>
    </div>
    <div class="layout">
      <grid-layout
        :layout="layout"
        :auto-size="false"
        :col-num="4"
        :row-height="84"
        :max-rows="100"
        :is-draggable="true"
        :is-resizable="true"
        :vertical-compact="false"
        :margin="[10, 10]"
        :use-css-transforms="true"
        @layout-updated="layoutUpdatedEvent">
        <grid-item v-for="item in layout" :key="item.i"
                   :x="item.x"
                   :y="item.y"
                   :w="item.w"
                   :h="item.h"
                   :i="item.i"
                   @resize="resizeEvent"
                   @move="moveEvent"
                   @resized="resizedEvent"
                   @moved="movedEvent">
          {{item.i}}
        </grid-item>
      </grid-layout>
    </div>
  </div>
</template>

<script>
import GridLayout from '../drag/GridLayout'
import GridItem from '../drag/GridItem'

var testLayout = [
  {'x': 0, 'y': 0, 'w': 1, 'h': 1, 'i': '0'},
  {'x': 1, 'y': 0, 'w': 1, 'h': 1, 'i': '1'},
  {'x': 2, 'y': 0, 'w': 1, 'h': 1, 'i': '2'},
  {'x': 0, 'y': 1, 'w': 1, 'h': 1, 'i': '3'},
  {'x': 1, 'y': 1, 'w': 1, 'h': 1, 'i': '4'},
  {'x': 2, 'y': 1, 'w': 1, 'h': 1, 'i': '5'},
  {'x': 0, 'y': 2, 'w': 1, 'h': 1, 'i': '6'},
  {'x': 1, 'y': 2, 'w': 1, 'h': 1, 'i': '7'},
  {'x': 2, 'y': 2, 'w': 1, 'h': 1, 'i': '8'}
]
export default {
  name: 'HelloWorld',
  components: {
    GridLayout,
    GridItem
  },
  data () {
    return {
      layout: testLayout
    }
  },
  methods: {
    watchitem: function (item) {
      /* if(item.y>y_max ||item.x>x_max){
          item.y=
            item.x=
        }
        return item */
    },
    moveEvent: function (i, newX, newY, e) {
      // console.log(e)
      // console.log("MOVE i=" + i + ", X=" + newX + ", Y=" + newY);
    },
    resizeEvent: function (i, newH, newW) {
      // console.log("RESIZE i=" + i + ", H=" + newH + ", W=" + newW);
    },
    movedEvent: function (i, newX, newY, e) {
      // console.log(e)
      // console.log("MOVED i=" + i + ", X=" + newX + ", Y=" + newY);
    },
    resizedEvent: function (i, newH, newW, newHPx, newWPx) {
      console.log('RESIZED i=' + i + ', H=' + newH + ', W=' + newW + ', H(px)=' + newHPx + ', W(px)=' + newWPx)
    },
    layoutUpdatedEvent: function (newLayout) {
      console.log('Updated layout: ', newLayout)
    },
    updateLayout (i) {
      let obj = this.layout.find(m => m.i === i)
      obj.x = obj.x + 1
      obj.y = obj.y + 1
    },
    deleteLayout (i) {
      let index = 0
      for (index = 0; index < this.layout.length; index++) {
        if (this.layout[index].i === i) {
          break
        }
      }
      this.layout.splice(index, 1)
    }
  }
}
</script>
<style>
  .vue-grid-layout div{
    background-color: #8ef4a6;
  }
</style>
