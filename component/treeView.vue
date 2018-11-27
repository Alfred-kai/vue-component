<template>
  <div class="cascade-wrap">
    <div v-for="(item,index) in treeList" :key="item.value" class="cascade-option">
      <span class="option-circle-level">{{ index+1 }}</span>
      <span class="ant-input-wrapper"><input v-model="item.label" class="ant-input ant-input-sm key-input option-margin" type="text" placeholder="输入选项"></span>
      <span class="fa fa-plus-circle" @click="addChildOption(item)"/>
      <span class="fa fa-remove " @click="deleteCascadeOption(treeList,index)"/>

      <div v-if="item.children && item.children.length" style="margin-left:30px">
        <tree-view :tree-list="item.children" @add="addInner" @del="delInner"/>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'TreeView',
  props: {
    treeList: {
      type: Array,
      default: () => {
        return []
      }
    },
    parent: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  methods: {
    addChildOption(params) {
      this.$emit('add', params)
    },
    deleteCascadeOption(params, index) {
      const obj = {
        parent: params,
        index: index
      }
      this.$emit('del', obj)
    },
    addInner(params) {
      this.addChildOption(params)
    },
    delInner(params) {
      this.deleteCascadeOption(params)
    }
  }
}
</script>
<style scoped>
.cascade-wrap .cascade-option {
  border-bottom: dashed 1px #ddd;
  padding-bottom: 10px;
  padding-top: 5px;
}
.cascade-wrap span {
  color: #6c7480;
  display: inline-block;
}
.cascade-wrap .option-circle-level {
  border-radius: 100%;
  width: 20px;
  line-height: 18px;
  text-align: center;
  display: inline-block;
  border: 1px solid #999;
}

.cascade-wrap .option-margin {
  margin-left: 6px;
}
.cascade-wrap .key-input {
  width: 200px;
  margin-top: 8px;
  border: 1px solid #d5ddeb;
  border-radius: 2px;
  background: #fff;
  color: #4c5159;
}

.ant-input {
  position: relative;
  display: inline-block;
  padding: 4px 7px;
  width: 100%;
  height: 28px;
  cursor: text;
  font-size: 12px;
  line-height: 1.5;
  color: #666;
  background-color: #fff;
  background-image: none;
  border: 1px solid #d9d9d9;
  border-radius: 6px;
  -webkit-transition: border 0.2s cubic-bezier(0.645, 0.045, 0.355, 1),
    background 0.2s cubic-bezier(0.645, 0.045, 0.355, 1),
    box-shadow 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
  transition: border 0.2s cubic-bezier(0.645, 0.045, 0.355, 1),
    background 0.2s cubic-bezier(0.645, 0.045, 0.355, 1),
    box-shadow 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
}
.dustbin-button {
  font-size: 14px;
  width: 20px;
  height: 20px;
  line-height: 20px;
  background-color: #e9edf2;
  color: #acb3bf;
  text-align: center;
  cursor: pointer;
  transition: all 0.5s;
}
.icon-shanchu {
  color: #2db7f5;
  cursor: pointer;
  margin-left: 6px;
}
.icon-tianjiaxiao:before {
  vertical-align: -3px;
  font-size: 20px;
}
</style>
