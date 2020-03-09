<template>
  <div style="background:#ECECEC; padding:10px;text-align:left">
    <a-card :title="notice.title" :bordered="false" style="width: 400px">
      <p>{{notice.title }}
       <span class="spanStyle" style="float:right;cursor:pointer" @click="look">查看全部></span>
       </p>
      <p v-for="item in noticeData">
      <span class="spanStyle">{{item.floor}}</span>
      <span class="spanStyle">{{item.type}}</span>
      <span class="spanStyle"  :class="{redColor:item.notice=='高温警告'}">{{item.notice}}</span>
      <span class="spanStyle">{{item.time}}</span>
      </p>
    </a-card>
    <Son :noticeModal="noticeModal" :sendNotice='sendNotice' @closeModal="closeModal"></Son>
  </div>
</template>
<script>
    import Son from './son'
    export default {
        name: "main-header",
        components:{
            Son
        },
        data(){
            return{
                sendNotice:{},
                noticeData:[],
                noticeModal:false,
                notice:{
                    title:"告警信息",
                    data:[
                      {
                        floor:'10F',
                        type:"电气设备 A2430XX",
                        notice:'高温警告',
                        time:"14:15:28"
                      },
                      {
                        floor:'13F',
                        type:"电气设备 A2030XX",
                        notice:'离线警告',
                        time:"14:45:28"
                      },
                      {
                        floor:'14F',
                        type:"电气设备 A2070XX",
                        notice:'高温警告',
                        time:"14:35:28"
                      },
                      {
                        floor:'13F',
                        type:"电气设备 A2030XX",
                        notice:'离线警告',
                        time:"14:45:28"
                      },
                      {
                        floor:'14F',
                        type:"电气设备 A2070XX",
                        notice:'高温警告',
                        time:"14:35:28"
                      }
                    ]
                },
            }
        },
        methods:{
            look(){
                this.noticeModal=true
                this.sendNotice=this.notice
            },
            closeModal(x){
                this.noticeModal=false
                this.sendNotice={}
            }
        },
        created(){
            this.noticeData=this.notice.data.slice(0,2)
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
