<template>
  <div>
      <input type="text" @keyup.enter="add" placeholder="请输入你想做的事情" v-model="input">
      <br><br><br>
      <div v-if="todoList.length===0">还没有待办事项<br><br></div>
      <div v-for="(item,index) in todoList" :key="item.key" v-if="(no==false && yes==false)==true ? 1 : yes ? item.check : !item.check">
            <input :checked="item.check" @change="checked(index)" type="checkbox">
            <span v-if="!item.check">{{item.name}}</span>
            <s v-else>{{item.name}}</s>
            <button @click="remove(index)">删除</button>
            <br><br>
      </div>

      <button v-if="todoList.length>0" @click="c(1)"><span v-if="yes">👿</span>只看完成了的</button>
      <button v-if="todoList.length>0" @click="c(2)"><span v-if="no">👿</span>只看未完成的</button>
      <button v-if="todoList.length>0" @click="c(3)"><span v-if="(!yes && !no)==true ? 1 : 0">👿</span>查看全部的</button>
  </div>
</template>
<script>
    export default{
        data(){
            return {
                input:null,
                todoList:[],
                yes:false,
                no:false,
            }
        },
        methods:{
            add(){
                this.todoList.push({name:this.input,check:false});
                this.input = null;
            },
            remove(index){
                this.todoList.splice(index,1);
            },
            checked(index){
                this.todoList[index].check = !this.todoList[index].check;
            },
            c(i){
                if(i==1){
                    this.yes = !this.yes;
                    this.no = !this.yes;
                }
                if(i==2){
                    this.no = !this.no;
                    this.yes = !this.no;
                }
                if(i==3){
                    this.no = false;
                    this.yes = false;
                }

                console.log('yes:'+this.yes+',no:'+this.no);
            }
        }
    }
</script>