<template>
  <div class="home">
    <a-table :columns="columns" :dataSource="stuData" bordered>
    <template slot="name" slot-scope="text">
      <a href="javascript:;">{{text}}</a>
    </template>
    <a slot="action" slot-scope="text, record" @click="showModal(record)">action</a>
  </a-table>
     <a-modal :title="dataRow.name" v-model="visible" @ok="handleOk">
      <a-list
      v-if="comments.length"
      :dataSource="comments"
      :header="`${comments.length} ${comments.length > 1 ? 'replies' : 'reply'}`"
      itemLayout="horizontal"
    >
      <a-list-item slot="renderItem" slot-scope="item, index">
        <a-comment
          :author="item.author"
          :avatar="item.avatar"
          :content="item.content"
          :datetime="item.datetime"
        >
        <template slot="actions">
          <span>
            <a-tooltip title="Like">
              <a-icon type="like" :theme="item.action === 'liked' ? 'filled' : 'outlined'" @click="like(index)" />
            </a-tooltip>
            <span style="padding-left: '8px';cursor: 'auto'">
              {{item.likes}}
            </span>
          </span>
          <span>
            <a-tooltip title="Dislike">
              <a-icon
                type="dislike"
                :theme="item.action === 'disliked' ? 'filled' : 'outlined'"
                @click="dislike(index)"
              />
            </a-tooltip>
            <span style="padding-left: '8px';cursor: 'auto'">
              {{item.dislikes}}
            </span>
          </span>
          <span v-if="!item.addAuthor" @click="reply(index)">Reply to</span>
          <a-tooltip v-if="item.addAuthor" title="已经有了一个Reply to">
             Reply to
          </a-tooltip>
        </template>
        <a-comment v-if="item.addAuthor"
          :author="item.addAuthor"
          :avatar="item.addAvatar"
          :content="item.addContent"
          :datetime="item.addDatetime"
        >
        </a-comment>
        </a-comment>
      </a-list-item>
    </a-list>
    <a-comment>
      <a-avatar
        slot="avatar"
        src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"
        :alt="dataRow.name"
      />
      <div slot="content">
        <a-form-item>
          <a-textarea :rows="4" @change="handleChange" :value="value"></a-textarea>
        </a-form-item>
        <a-form-item>
          <a-button htmlType="submit" :loading="submitting" @click="handleSubmit" type="primary">
            Add Comment
          </a-button>
        </a-form-item>
      </div>
    </a-comment>
    </a-modal>


    <a-modal title="reply" v-model="replyModal" :footer="null">
    <a-comment>
      <a-avatar
        slot="avatar"
        src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png"
        :alt="dataRow.name"
      />
      <div slot="content">
        <a-form-item>
          <a-textarea :rows="4" @change="replyHandleChange" v-model="Value"></a-textarea>
        </a-form-item>
        <a-form-item>
          <a-button htmlType="submit" :loading="replySubmitting" @click="replyHandleSubmit" type="primary">
            Add Comment
          </a-button>
        </a-form-item>
      </div>
    </a-comment>
    </a-modal>

  </div>
</template>

<script lang="ts">
import Vue from "vue";
import moment from 'moment';
 const renderContent = (value, row, index) => {
    const obj = {
      children: value,
      attrs: {},
    };

    return obj;
  };

  let data = [
    {
      key: '1',
      id: 1,
      name: '张三',
      subject: '语文',
      level: '中等',
      grade: 85,
    },{
      key: '2',
      id: 2,
      name: '李四',
      subject: '数学',
      level: '中等',
      grade: 23,
    }, {
      key: '3',
      id: 3,
      name: '张三',
      subject: '数学',
      level: '中等',
      grade: 63,
    },
    {
      key: '5',
      id: 5,
      name: '张三',
      subject: '英语',
      level: '中等',
      grade: 63,
    },
    {
      key: '4',
      id: 4,
      name: '李四',
      subject: '数学',
      level: '中等',
      grade: 23,
    },
  ];
const dealWithData = function(data) {
  let c = [];
  let d = {};
  let arr = [];

  data.forEach((element, indexs) => {
    if (!d[element.name]) {
      c.push({
        name: element.name,
        allData: [element],
        len: 0
      });
      d[element.name] = element;
    } else {
      
      c.forEach((ele, index) => {
        if (ele.name == element.name) {
          ele.allData.push(element); 
        }
      });

    }
  });
  
  c.forEach(el => {
    el.allData.forEach((ele,index) => {
      if(index == 0) {
        ele.len = el.allData.length
      } else {
        ele.len = 0
      }
    })
    arr.push(...el.allData)
  })
  return arr;
}
let stuData = dealWithData(data)
export default Vue.extend({
  name: "home",
  data() {
    const columns = [
        {
          title: '姓名',
          dataIndex: 'name',
          customRender: (value, row, index) => {
            const obj = {
              children: value,
              attrs: {},
            };
            obj.attrs.rowSpan = stuData[index].len;
            return obj;
          },
        },
        {
          title: '学科',
          dataIndex: 'subject',
          customRender: renderContent,
        },
        {
          title: '难度',
          dataIndex: 'level',
        },
        {
          title: '得分',
          dataIndex: 'grade',
          customRender: renderContent,
        },
         {
           title: '操作列',
           dataIndex: 'options',
           key: 'operation',
           scopedSlots: { customRender: 'action' },
         },
      ];
    return {
      stuData,
      columns,
      visible: false,
      dataRow:{},
      comments: [],
        submitting: false,
        replySubmitting:false,
        value: '',
        Value:'',
    
        moment,
        likes: 0,
        dislikes: 0,
        action: null,
        replyModal:false,
        replyIndex:null,
    }
  },
   methods: {
      showModal(record) {
        this.comments=[]
        this.visible = true;
        console.log(record)
        this.dataRow=record
      },
      handleOk(e) {
        console.log(e);
        this.visible = false;
      },
      handleSubmit() {
        if (!this.value) {
          return;
        }

        this.submitting = true;

        setTimeout(() => {
          this.submitting = false;
          this.comments = [
            {
              author: this.dataRow.name,
              avatar: 'https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png',
              content: this.value,
              datetime: moment().fromNow(),
              likes : 0,
              dislikes : 0,
              action : ' ',
              addAuthor: '',
              addAvatar: '',
              addContent: '',
              addDatetime: '',
            },
            ...this.comments,
          ];
          this.value = '';
        }, 1000);
      },
       replyHandleSubmit() {
        if (!this.Value) {
          return;
        }

        this.replySubmitting = true;

        setTimeout(() => {
          this.replySubmitting = false;
          this.comments[this.replyIndex].addAuthor=this.dataRow.name
          this.comments[this.replyIndex].addAvatar='https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png'
          this.comments[this.replyIndex].addContent=this.Value
          this.comments[this.replyIndex].addDatetime=moment().fromNow()
          this.replyModal=false
        }, 1000);
        
        this.Value = '';
      },
      handleChange(e) {
        this.value = e.target.value;
      },
      replyHandleChange(e) {
        this.replyValue = e.target.replyValue;
      },
      like(index) {
       
        this.comments[index].likes = 1;
        this.comments[index].dislikes = 0;
        this.comments[index].action = 'liked';
      },
      dislike(index) {
        this.comments[index].likes = 0;
        this.comments[index].dislikes = 1;
        this.comments[index].action = 'disliked';
      },
      reply(index){
        this.replyModal=true
        this.replyIndex=index
         console.log(this.replyIndex)
      }
    },
    
});
</script>
