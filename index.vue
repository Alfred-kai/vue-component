<template>
  <div style="padding:12px;">
    <div style="border:1px solid lime;">
      <tree-view :tree-list="treeList" @add="addTest" @del="delTest"/>
    </div>
  </div>
</template>
<script>
import treeView from './component'

const treeList = [
  {
    id: '0',
    label: '',
    children: [
      {
        id: '1.1',
        label: '',
        children: [
          {
            id: '1.1.1',
            label: '',
            children: []
          }
        ]
      }, {
        id: '1.2',
        label: '',
        children: []
      }
    ]
  }
]

const layout = []
export default {
  name: 'Test',
  components: {treeView },
  data() {
    return {
      treeList,
      layout
    }
  },
  methods: {
    addTest(params) {
      params.children.push({ 'label': '', 'children': [] })
    },
    delTest(params) {
      this.findChildren(params)
    },
    findChildren(obj) {
      if (obj.parent instanceof Array) {
        obj.parent.splice(obj.index, 1)
      } else {
        this.findChildren(obj.parent)
      }
    }
  }
}
</script>





