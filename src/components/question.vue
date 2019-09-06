<template>
  <div>
    <div id="top">
      <div class="header">
        <ul>
          <li>单选</li>
          <li>多选</li>
          <li>填空</li>
          <li>矩阵</li>
        </ul>
      </div>
      <div class="read">预览</div>
    </div>
    <div class="listbox">
      <ul>
        <li v-for="(val,index) of listdata" :key="index" @mouseenter="enter(index)" @mouseleave="out" :class="{'active':selected==index}">
          <div class="topbox">
            <div class="tbox">
              <span class="number">{{index+1}}.</span>
              <span class="title">{{val.title}}</span>
              <span class="type">【{{typename(val.type)}}】</span>
            </div>
            <div class="">
              
            </div>
          </div>
         
         <div class="tips" v-show="index==selected">
           <span @click="up(index)">上移</span>
           <span @click="down(index)">下移</span>
           <span @click="edit(index)">编辑</span>
           <span @click="del(index)">删除</span>
         </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        selected:null,
        listdata:[
          {title:'11111111',type:"1",list:[]},
          {title:'22222222',type:"2",list:[]},
          {title:'333333333',type:"3",list:[]}
        ]
      }
    },
    methods: {
      dxuan(){
        this.listdata.push({title:'55555',type:"3",list:[]})
      },
      up(index){//上移
        if(!index) return;
        let currentdata=this.listdata.slice(index,index+1)[0];
        let prevdata=this.listdata.slice(index-1,index)[0];
        this.$set(this.listdata,index,prevdata);
        this.$set(this.listdata,index-1,currentdata);
      },
      down(index){//下移
        if(index==this.listdata.length-1) return;
        let currentdata=this.listdata.slice(index,index+1)[0];
        let nextdata=this.listdata.slice(index+1,index+2)[0];
        this.$set(this.listdata,index,nextdata);
        this.$set(this.listdata,index+1,currentdata);
      },
      enter(index){//鼠标移入
        this.selected=index;
      },
      out(){//鼠标移出
        this.selected=null;
      },
      del(index){//删除
        this.listdata.splice(index,index+1);
      },
      edit(index){

      },
      typename(n){//类型判断
        switch(n){
          case '1':
            return '单选'
            break;
          case '2':
            return '多选'
            break;
          case '3':
            return '填空'
            break;
          case '4':
            return '矩阵'
            break;
        }
      }
    },
  }
</script>

<style lang="scss" scoped>
#top{
 	position: fixed;
 	top:0;
 	left: 0;
 	right: 0;
 	background: #888;
 	z-index: 999;
 }

.header{
	width: 60%;
	margin:20px auto;
	background: #0095da;
	border-radius: 10px;

}
.read{
	position: absolute;
	top:33px;
	right: 40px;
	width:100px;
	height: 30px;
	background: red;
	color: #fff;
	text-align: center;
	border-radius: 20px;
	cursor: pointer;
}
.header ul{
	display: flex;
	width:100%;
	align-items:center;
}
.header ul li{
	height:50px;
	line-height: 50px;
	width:60px;
	color:#fff;
	text-align: center;
	cursor: pointer;
}
.header ul li:hover{
	background:green;
	color:#f58220;
}
.listcen{
	display: flex;
	align-items:center;
}
.listcen>li{
		display: flex;
	align-items:center;
	justify-content:center;
	flex: 1;
}
#savelist{
	display: flex;
	align-items :center;
	justify-content: center;
	width:100px;
	height: 50px;
	background: #0095da;
	border-radius:10px;
	cursor: pointer;
	color:#fff;
	margin-top:30px;
	margin:30px auto 0;
}
.serinput{
	
	flex: 2;
}
.listbox{
  width: 660px;
  font-size: 14px;
  color: rgb(51, 51, 51);
  margin: 100px auto 0px;
}
.listbox ul li{
  position: relative;
  z-index: 8;
  border: 2px solid #fff;
  padding: 0 5px;
  margin-top: 10px;
}
.listbox ul .active{
  border: 2px solid #0099ff;
}
.topbox{
  margin-top: 10px;
  margin-bottom: 20px;
}

.listbox ul li .type{
  color: #026fda;
}
.listbox ul li .tips{
  position: absolute;
  top: 5px;
  right: 5px;
}
.listbox ul li .tips span{
  display: inline-block;
  font-size: 12px;
  padding: 4px 10px;
  background: #0099ff;
  color: #fff;
  margin-left: 5px;
  cursor: pointer;
}





</style>