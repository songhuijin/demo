<template>
  <a-layout id="components-layout-demo-top" class="layout">
    <a-layout-header>
      <a-menu
        theme="dark"
        mode="horizontal"
        :selectedKeys="[this.$route.path]"
        :defaultSelectedKeys="SelectedKeys"
        :style="{ lineHeight: '64px' }"
        @select="selectMenu"
      >
        <a-menu-item key="/">题目一、题目二</a-menu-item>
        <a-menu-item key="/about">题目三-题目十二</a-menu-item>
        <a-menu-item key="/parent">父子传值</a-menu-item>
      </a-menu>
    </a-layout-header>
    <a-layout-content>
      <div :style="{ background: '#fff',  minHeight: '280px' }">
       <router-view></router-view>
      </div>
    </a-layout-content>
  </a-layout>
</template>
<style>
  
</style>
<script>
    export default {
        name: "main-header",
        data(){
            return{
                SelectedKeys:['/'],
            }
        },
        methods:{
            selectMenu(key){
                if(key.key=='/'){
                    this.SelectedKeys[0]='/'
                    this.$router.push({path:'/'})
                }
                if(key.key=='/about'){
                    this.SelectedKeys[0]='/about'
                    this.$router.push({path:'/about'})
                }
                if(key.key=='/parent'){
                    this.SelectedKeys[0]='/parent'
                    this.$router.push({path:'/parent'})
                }
            }
        }
    }
</script>