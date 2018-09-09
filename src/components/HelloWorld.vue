<template>
  <div class="hello">
    <el-tree :data="data"
    node-key="id"
    :default-checked-keys="selected"
    :default-expanded-keys="expanded"
    ref="tree"
    show-checkbox>
    </el-tree>
    <br>
    <el-button type="danger" @click="getSelected">click</el-button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      data:[
        {
          id:1,
          label:'11',
          properties:{
            checked:0
          },
          children:[
            {
              id:2,
              label:'喵帕斯',
              properties:{
                checked:0
              },
              children:[
                {
                  id:3,
                  label:'aa',
                  properties:{
                    checked:0
                  },
                },
                {
                  id:8,
                  label:'aa',
                  properties:{
                    checked:1
                  },
                },
                {
                  id:4,
                  label:'bb',
                  properties:{
                    checked:1
                  },
                }
              ]
            }
          ]
        },
        {
          id:5,
          label:'bb',
          properties:{
            checked:1
          },
        }
      ],
      selected:[],
      expanded:[]
    }
  },
  created(){
    this.getChecked()
  },
  methods:{
    getChecked(){
      if(Array.isArray(this.data)) {
        this.data.forEach(node=>{
          // console.log(node)
          this.getCheckedNodes(node)
        })
      }
      console.log(this.selected)
    },
    getCheckedNodes(node){
      console.log(node)
      if(node.children){
        // this.getCheckedNodes(node.children)
        node.children.forEach(item=>{
          this.getCheckedNodes(item)
        })
      } else if(node.properties.checked===1){
        this.selected.push(node.id)
      }
    },
    getSelected(){
      let checked=this.$refs.tree.getCheckedKeys().concat(this.$refs.tree.getHalfCheckedKeys())

      console.log(checked)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div.hello{
  display: flex;
  justify-content: space-around;
}
</style>
