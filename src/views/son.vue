<template>
  <a-modal :title="notice.title" 
  v-model="visible" 
  :footer="null"
   :maskClosable="false"
   @cancel="cancelMethod"
   >
    <a-card  :bordered="false" style="width: 400px">
      <p v-for="item in notice.data">
      <span class="spanStyle">{{item.floor}}</span>
      <span class="spanStyle">{{item.type}}</span>
      <span class="spanStyle"  :class="{redColor:item.notice=='高温警告'}">{{item.notice}}</span>
      <span class="spanStyle">{{item.time}}</span>
      </p>
    </a-card>
  </a-modal>
</template>
<script>
    export default {
        name: "",
        props:{
            noticeModal:Boolean,
            sendNotice:Object
        },
        data(){
            return{
                visible: false,
                notice:{
                },
            }
        },
        methods:{
            cancelMethod(status){
                this.visible=false
                console.log(status)
                this.$emit("closeModal",'false')
            }
        },
        watch:{
            noticeModal(){
                this.visible=this.noticeModal
                this.notice=this.sendNotice
            },
            
        }
    }
</script>
<style>
 .spanStyle{
   display:inline-block;
   padding:0 10px;
 }
 .redColor{
     color:red
 }
</style>
