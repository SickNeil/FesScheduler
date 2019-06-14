<template>
  <div id="app">
    <div v-for="date in dates" :key="date.index">
      <h1>{{date.title}}</h1><span>{{date.date}}</span>
      <div v-for="stage in stages" :key="stage.index">        
        <h2>{{stage.name}}</h2>
        <div v-for="schedule in getSchedules(date.index, stage.index)" :key="schedule.index">    
          <span class="performer">{{schedule.performer}}</span> 
          <span class="startTime">{{schedule.startTime}}</span> 
          <span class="endTime">{{schedule.endTime}}</span>  
          <span class="remark">{{schedule.remark}}</span> 
          <span class="country">{{schedule.country}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'

let config = {
    apiKey: "AIzaSyBgTTgX9Fui1pcbWmWaYj2WB4v2gOhha9M",
    authDomain: "fesscheduler.firebaseapp.com",
    databaseURL: "https://fesscheduler.firebaseio.com",
    projectId: "fesscheduler",
    storageBucket: "fesscheduler.appspot.com",
    messagingSenderId: "1179700144",
    appId: "1:1179700144:web:2a117270b4946a20"
};
let app = Firebase.initializeApp(config);
let db = app.database();

let dates = [
  { index: 1, date: "2019.01.25", title: "DAY1" }, 
  { index: 2, date: "2019.01.26", title: "DAY2" }, 
  { index: 3, date: "2019.01.27", title: "DAY3" },
];
let stages = [
  { index: 1, name: "大龍山", },
  { index: 2, name: "大圓山", },
  { index: 3, name: "大稻埕", },
  { index: 4, name: "大拇哥", },
  { index: 5, name: "大聲公", },
  { index: 6, name: "大草原", },
  { index: 7, name: "Legacy STAGE", },
  { index: 8, name: "The Wall STAGE", },
  { index: 9, name: "PIPE STAGE", },
  { index: 10, name: "Revolver STAGE", },
  { index: 11, name: "ROXY VIBE STAGE", },
  { index: 12, name: "海邊的卡夫卡 STAGE", },
  { index: 13, name: "小地方 STAGE", },
  { index: 14, name: "樂悠悠之口 STAGE", },
];
let schedules = [
  { index: 1, dateIdx: 1, stageIdx: 1, startTime: "17:20", endTime: "18:00", performer: "美秀集團", country: "", remark: "" },
  { index: 2, dateIdx: 1, stageIdx: 1, startTime: "19:20", endTime: "20:00", performer: "The Birthday", country: "JP", remark: "" },
  { index: 3, dateIdx: 1, stageIdx: 1, startTime: "21:20", endTime: "22:00", performer: "茄子蛋", country: "", remark: "" },
  { index: 4, dateIdx: 1, stageIdx: 2, startTime: "16:20", endTime: "17:00", performer: "Lucie,Too", country: "JP", remark: "" },
  { index: 5, dateIdx: 1, stageIdx: 2, startTime: "18:20", endTime: "19:00", performer: "夜貓外傳", country: "", remark: "春艷、Leo王" },
  { index: 6, dateIdx: 1, stageIdx: 2, startTime: "20:20", endTime: "21:00", performer: "I Mean Us", country: "", remark: "" },
  { index: 7, dateIdx: 1, stageIdx: 4, startTime: "18:00", endTime: "18:40", performer: "胖虎", country: "", remark: "" },
  { index: 8, dateIdx: 1, stageIdx: 4, startTime: "19:20", endTime: "20:00", performer: "非人物種", country: "", remark: "" },
  { index: 9, dateIdx: 1, stageIdx: 4, startTime: "20:40", endTime: "21:20", performer: "929", country: "", remark: "" },
  { index: 10, dateIdx: 1, stageIdx: 5, startTime: "17:20", endTime: "18:00", performer: "黎可辰", country: "", remark: "" },
  { index: 11, dateIdx: 1, stageIdx: 5, startTime: "18:40", endTime: "19:20", performer: "Peter Fish", country: "", remark: "" },
  { index: 12, dateIdx: 1, stageIdx: 5, startTime: "20:00", endTime: "20:40", performer: "莫宰羊", country: "", remark: "" },
  { index: 13, dateIdx: 1, stageIdx: 5, startTime: "21:20", endTime: "22:00", performer: "DJ 陳玠安", country: "", remark: "" },
  { index: 14, dateIdx: 1, stageIdx: 6, startTime: "18:00", endTime: "18:40", performer: "渣泥", country: "", remark: "" },
  { index: 15, dateIdx: 1, stageIdx: 6, startTime: "19:20", endTime: "20:00", performer: "魏嘉瑩", country: "", remark: "& Arrow Band" },
  { index: 16, dateIdx: 1, stageIdx: 6, startTime: "20:40", endTime: "21:20", performer: "DSPS", country: "", remark: "" },
  { index: 17, dateIdx: 2, stageIdx: 1, startTime: "11:20", endTime: "12:00", performer: "Vast & Hazy", country: "", remark: "" },
  { index: 18, dateIdx: 2, stageIdx: 1, startTime: "13:20", endTime: "14:00", performer: "安溥", country: "", remark: "" },
  { index: 19, dateIdx: 2, stageIdx: 1, startTime: "15:20", endTime: "16:00", performer: "MOROHA", country: "JP", remark: "" },
  { index: 20, dateIdx: 2, stageIdx: 1, startTime: "17:20", endTime: "18:00", performer: "舒米恩", country: "", remark: "" },
  { index: 21, dateIdx: 2, stageIdx: 1, startTime: "19:20", endTime: "20:00", performer: "Hello Nico", country: "", remark: "" },
  { index: 22, dateIdx: 2, stageIdx: 1, startTime: "21:20", endTime: "22:00", performer: "新褲子", country: "JP", remark: "" },
];

export default {
  name: 'App',
  data(){
    return {
      dates: dates,
      stages: stages,
      schedules: schedules,
    }
  },
  methods: {
    getSchedules(dateIdx, stageIdx){
      return this.schedules.filter(m => m.dateIdx == dateIdx && m.stageIdx == stageIdx);
    },
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
