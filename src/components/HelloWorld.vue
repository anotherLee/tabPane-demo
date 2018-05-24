<template>
  <div class="hello">
    <ul class="leftList">
      <li v-for="item in leftList" :key="item.id" @click="leftClick(item.id, item.name)">{{item.name}}</li>
    </ul>
    <div class="tabPane">
      <ul class="tabMenu">
        <li class="title" v-for="item in tabs" :key="item.name" :class="{actived: item.id === currentTab}" @click="switchTab(item.id)">{{item.name}}</li>
        <span class="clear" v-if="tabs.length > 0" @click="clear">清空</span>
      </ul>
      <ul class="tabContent">
        <li class="content" v-for="item in tabs" :key="item.name" v-show="currentTab === item.id">{{item.content}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      leftList: [
        { id: 1, name: '小明' },
        { id: 2, name: '小张' },
        { id: 3, name: '小强' },
        { id: 4, name: '小武' },
        { id: 5, name: '小红' }
      ],
      tabs: [
        { id: 1, name: '小明', content: '小明的content' },
        { id: 2, name: '小张', content: '小张的content' }
      ],
      currentTab: 1
    }
  },
  methods: {
    leftClick(id, name) {
      let res = this.tabs.find(item => {
        return item.id === id && item.name === name
      })
      if (res) {
        this.currentTab = this.currentTab = res.id
      } else {
        this.tabs.push({
          id,
          name,
          content: `${name}的content`
        })
        this.currentTab = id
      }
    },
    switchTab(id) {
      this.currentTab = id
    },
    clear() {
      this.tabs.splice(0)
    }
  }
}
</script>

<style scoped lang="scss">
@mixin actived{
  background-color: #ddd;
}
.hello{
  display: flex;
  width: 800px;
  height: 400px;
  margin: 0 auto;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 0 4px #dcdcdc;
  .leftList{
    width: 30%;
    padding-top: 15px;
    border-right: 1px solid #ddd;
    >li{
      padding: 5px 20px;
      cursor: pointer;
      &:hover{
        background-color: #dcdcdc;
      }
    }
  }
  .tabPane{
    flex: 1;
    >.tabMenu{
      display: flex; align-items: center;
      height: 10%;
      border-bottom: 1px solid #ddd;
      >li{
        display: flex;
        justify-content: center; align-items: center;
        height: 100%;
        padding: 0 10px;
        cursor: pointer;
        &:hover{
          @include actived;
        }
      }
      >.actived{
        @include actived;
      }
      >.clear{
        display: inline-block;
        padding: 2px 5px; margin-left: 15px;
        border: 1px solid #ddd; border-radius: 3px;
        cursor: pointer;
      }
    }
    >.tabContent{
      height: 90%;
      width: 100%;
      >li{
        width: 100%;
        height: 100%;
      }
    }
  }
}
</style>
