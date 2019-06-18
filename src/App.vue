<template>
  <div id="app">
    <div v-for="date in dates" :key="date.index">
      <h1>{{date.title}}</h1><span>{{date.date}}</span>
      <div v-for="stage in stages" :key="stage.index">        
        <h2>{{stage.name}}</h2>
        <div v-for="schedule in getSchedules(date.index, stage.index)" :key="schedule.index">    
          <span class="performer">{{schedule.performer}}</span> 
          <span class="startTime">{{schedule.startTime}}</span> - <span class="endTime">{{schedule.endTime}}</span>            
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
  { index: 1, date: "2019.07.05", title: "DAY1" }, 
  { index: 2, date: "2019.07.06", title: "DAY2" }, 
  { index: 3, date: "2019.07.07", title: "DAY3" },
];
let stages = [
  { index: 1, name: "射日", engName: "SUN-SHOOTING" },
  { index: 2, name: "眠月", engName: "MIANYUE" },
  { index: 3, name: "澄波", engName: "CHENG-PO STAGE" },
  { index: 4, name: "七虎", engName: "SEVEN TIGERS" },
  { index: 5, name: "站出來", engName: "STAND UP" },
  { index: 6, name: "愛玉子", engName: "AIYU" },
  { index: 7, name: "春萌", engName: "CHUNMENG" },
  { index: 8, name: "山丘", engName: "HILL" },
  { index: 9, name: "電火雞", engName: "ELECTRO-TURKEY" },
  { index: 10, name: "Red Bull Stage", engName: "Red Bull Stage" },
];
let schedules = [
  { index: 1, dateIdx: 1, stageIdx: 1, startTime: "17:20", endTime: "18:00", performer: "董事長樂團 ft.黃鐙輝", country: "", remark: "" },
  { index: 2, dateIdx: 1, stageIdx: 1, startTime: "18:40", endTime: "19:20", performer: "傻子與白痴", country: "", remark: "" },
  { index: 3, dateIdx: 1, stageIdx: 1, startTime: "20:00", endTime: "20:40", performer: "Hello Nico", country: "", remark: "" },
  { index: 4, dateIdx: 1, stageIdx: 1, startTime: "21:20", endTime: "22:00", performer: "十年彩蛋", country: "", remark: "" },
  { index: 5, dateIdx: 1, stageIdx: 2, startTime: "16:40", endTime: "17:20", performer: "LEO37+5055", country: "", remark: "" },
  { index: 6, dateIdx: 1, stageIdx: 2, startTime: "18:00", endTime: "18:40", performer: "激膚", country: "", remark: "" },
  { index: 7, dateIdx: 1, stageIdx: 2, startTime: "19:20", endTime: "20:00", performer: "Trash", country: "", remark: "" },
  { index: 8, dateIdx: 1, stageIdx: 2, startTime: "20:40", endTime: "21:20", performer: "Frandé 法蘭黛樂團", country: "", remark: "" },
  { index: 9, dateIdx: 1, stageIdx: 3, startTime: "17:20", endTime: "18:00", performer: "イルカポリス 海豚刑警", country: "", remark: "" },
  { index: 10, dateIdx: 1, stageIdx: 3, startTime: "18:40", endTime: "19:20", performer: "全部君のせいだ", country: "JP", remark: "" },
  { index: 11, dateIdx: 1, stageIdx: 3, startTime: "20:00", endTime: "20:40", performer: "Crispy 脆樂團", country: "", remark: "" },
  { index: 12, dateIdx: 1, stageIdx: 3, startTime: "21:20", endTime: "22:00", performer: "PiA 吳蓓雅", country: "", remark: "" },
  { index: 13, dateIdx: 1, stageIdx: 4, startTime: "16:40", endTime: "17:20", performer: "椅子樂團 The Chairs", country: "", remark: "" },
  { index: 14, dateIdx: 1, stageIdx: 4, startTime: "18:00", endTime: "18:40", performer: "台青蕉", country: "", remark: "" },
  { index: 15, dateIdx: 1, stageIdx: 4, startTime: "19:20", endTime: "20:00", performer: "午夜乒乓", country: "", remark: "" },
  { index: 16, dateIdx: 1, stageIdx: 4, startTime: "20:40", endTime: "21:20", performer: "妖の鬼狐", country: "", remark: "" },
  { index: 16, dateIdx: 1, stageIdx: 5, startTime: "16:40", endTime: "17:20", performer: "緩緩", country: "", remark: "" },
  { index: 16, dateIdx: 1, stageIdx: 5, startTime: "18:00", endTime: "18:40", performer: "荷爾蒙少年", country: "", remark: "" },
  { index: 17, dateIdx: 1, stageIdx: 5, startTime: "19:20", endTime: "20:00", performer: "謎路人", country: "", remark: "" },
  { index: 18, dateIdx: 1, stageIdx: 5, startTime: "20:40", endTime: "21:20", performer: "TYNT", country: "", remark: "" },
  { index: 19, dateIdx: 1, stageIdx: 6, startTime: "17:20", endTime: "18:00", performer: "June Pan", country: "", remark: "" },
  { index: 20, dateIdx: 1, stageIdx: 6, startTime: "18:40", endTime: "19:20", performer: "奉獻之火", country: "", remark: "" },
  { index: 21, dateIdx: 1, stageIdx: 6, startTime: "20:00", endTime: "20:40", performer: "鐵擊", country: "", remark: "" },
  { index: 22, dateIdx: 1, stageIdx: 6, startTime: "21:20", endTime: "22:00", performer: "優雅逆轉", country: "", remark: "" },
  { index: 23, dateIdx: 1, stageIdx: 7, startTime: "16:40", endTime: "17:20", performer: "The コットンクラブ", country: "JP", remark: "" },
  { index: 24, dateIdx: 1, stageIdx: 7, startTime: "18:00", endTime: "18:40", performer: "ゲシュタルト乙女", country: "", remark: "" },
  { index: 25, dateIdx: 1, stageIdx: 7, startTime: "19:20", endTime: "20:00", performer: "百合花", country: "", remark: "" },
  { index: 26, dateIdx: 1, stageIdx: 7, startTime: "20:40", endTime: "21:20", performer: "唐貓", country: "", remark: "" },
  { index: 27, dateIdx: 1, stageIdx: 8, startTime: "17:20", endTime: "18:00", performer: "霧虹 Fogbow", country: "", remark: "" },
  { index: 28, dateIdx: 1, stageIdx: 8, startTime: "18:40", endTime: "19:20", performer: "暖嶼", country: "", remark: "" },
  { index: 29, dateIdx: 1, stageIdx: 8, startTime: "20:00", endTime: "20:40", performer: "南西肯恩", country: "", remark: "" },
  { index: 30, dateIdx: 1, stageIdx: 8, startTime: "21:20", endTime: "22:00", performer: "知更", country: "", remark: "" },
  { index: 31, dateIdx: 1, stageIdx: 9, startTime: "18:00", endTime: "18:40", performer: "Big & MEE", country: "", remark: "" },
  { index: 32, dateIdx: 1, stageIdx: 9, startTime: "19:20", endTime: "20:00", performer: "砂漠、爆発", country: "", remark: "" },
  { index: 33, dateIdx: 1, stageIdx: 9, startTime: "20:40", endTime: "21:20", performer: "IPHAZE", country: "", remark: "" },
  { index: 34, dateIdx: 1, stageIdx: 10, startTime: "16:10", endTime: "16:40", performer: "Hello Nico x 法蘭黛 Frandé", country: "", remark: "" },
  { index: 35, dateIdx: 1, stageIdx: 10, startTime: "16:50", endTime: "17:10", performer: "PiA 吳蓓雅 x Crispy 脆樂團", country: "", remark: "" },
  { index: 36, dateIdx: 1, stageIdx: 10, startTime: "18:00", endTime: "18:30", performer: "LEO37+5055", country: "", remark: "" },
  { index: 37, dateIdx: 2, stageIdx: 1, startTime: "12:00", endTime: "12:40", performer: "Vast & Hazy", country: "", remark: "" },
  { index: 38, dateIdx: 2, stageIdx: 1, startTime: "13:20", endTime: "14:00", performer: "旺福", country: "", remark: "" },
  { index: 39, dateIdx: 2, stageIdx: 1, startTime: "14:40", endTime: "15:20", performer: "拍謝少年", country: "", remark: "" },
  { index: 40, dateIdx: 2, stageIdx: 1, startTime: "16:00", endTime: "16:40", performer: "Slot Machine", country: "JP", remark: "" },
  { index: 41, dateIdx: 2, stageIdx: 1, startTime: "17:20", endTime: "18:00", performer: "茄子蛋", country: "", remark: "" },
  { index: 42, dateIdx: 2, stageIdx: 1, startTime: "18:40", endTime: "19:20", performer: "美秀集團", country: "", remark: "" },
  { index: 43, dateIdx: 2, stageIdx: 1, startTime: "20:00", endTime: "20:40", performer: "陳珊妮", country: "", remark: "" },
  { index: 44, dateIdx: 2, stageIdx: 1, startTime: "21:20", endTime: "22:00", performer: "閃靈", country: "", remark: "" },
  { index: 45, dateIdx: 2, stageIdx: 2, startTime: "12:40", endTime: "13:20", performer: "Leo王", country: "", remark: "" },
  { index: 46, dateIdx: 2, stageIdx: 2, startTime: "14:00", endTime: "14:40", performer: "怕胖團", country: "", remark: "" },
  { index: 47, dateIdx: 2, stageIdx: 2, startTime: "15:20", endTime: "16:00", performer: "隨性", country: "", remark: "" },
  { index: 48, dateIdx: 2, stageIdx: 2, startTime: "16:40", endTime: "17:20", performer: "老王樂團", country: "", remark: "" },
  { index: 49, dateIdx: 2, stageIdx: 2, startTime: "18:00", endTime: "18:40", performer: "胖虎", country: "", remark: "" },
  { index: 50, dateIdx: 2, stageIdx: 2, startTime: "19:20", endTime: "20:00", performer: "血肉果汁機", country: "", remark: "" },
  { index: 51, dateIdx: 2, stageIdx: 2, startTime: "20:40", endTime: "21:20", performer: "deca joins", country: "", remark: "" },
  { index: 52, dateIdx: 2, stageIdx: 3, startTime: "12:00", endTime: "12:40", performer: "麋先生", country: "", remark: "" },
  { index: 53, dateIdx: 2, stageIdx: 3, startTime: "13:20", endTime: "14:00", performer: "李友廷", country: "", remark: "" },
  { index: 54, dateIdx: 2, stageIdx: 3, startTime: "14:40", endTime: "15:20", performer: "Typecast", country: "PH", remark: "" },
  { index: 55, dateIdx: 2, stageIdx: 3, startTime: "16:00", endTime: "16:40", performer: "淺堤", country: "JP", remark: "" },
  { index: 56, dateIdx: 2, stageIdx: 3, startTime: "17:20", endTime: "18:00", performer: "小球", country: "", remark: "莊鶰瑛" },
  { index: 57, dateIdx: 2, stageIdx: 3, startTime: "18:40", endTime: "19:20", performer: "ANNALYNN", country: "TH", remark: "" },
  { index: 58, dateIdx: 2, stageIdx: 3, startTime: "20:00", endTime: "20:40", performer: "孔雀眼", country: "", remark: "" },
  { index: 59, dateIdx: 2, stageIdx: 3, startTime: "21:20", endTime: "22:00", performer: "七月半", country: "", remark: "" },
  { index: 60, dateIdx: 2, stageIdx: 4, startTime: "12:40", endTime: "13:20", performer: "猴子飛行員", country: "", remark: "" },
  { index: 61, dateIdx: 2, stageIdx: 4, startTime: "14:00", endTime: "14:40", performer: "必順鄉村", country: "", remark: "" },
  { index: 62, dateIdx: 2, stageIdx: 4, startTime: "15:20", endTime: "16:00", performer: "South Penguin", country: "JP", remark: "" },
  { index: 63, dateIdx: 2, stageIdx: 4, startTime: "16:40", endTime: "17:20", performer: "薄荷葉", country: "", remark: "" },
  { index: 64, dateIdx: 2, stageIdx: 4, startTime: "18:00", endTime: "18:40", performer: "EMERGING FROM THE COCOON", country: "", remark: "" },
  { index: 65, dateIdx: 2, stageIdx: 4, startTime: "19:20", endTime: "20:00", performer: "BRATS", country: "", remark: "" },
  { index: 66, dateIdx: 2, stageIdx: 4, startTime: "20:40", endTime: "21:20", performer: "夕陽武士", country: "", remark: "" },
  { index: 67, dateIdx: 2, stageIdx: 5, startTime: "12:00", endTime: "12:30", performer: "未", country: "", remark: "" },
  { index: 68, dateIdx: 2, stageIdx: 5, startTime: "12:50", endTime: "13:20", performer: "跨境巴士", country: "", remark: "" },
  { index: 69, dateIdx: 2, stageIdx: 5, startTime: "14:00", endTime: "14:40", performer: "渣泥 ZANI", country: "", remark: "" },
  { index: 70, dateIdx: 2, stageIdx: 5, startTime: "15:20", endTime: "16:00", performer: "黃子軒與山平快", country: "", remark: "" },
  { index: 71, dateIdx: 2, stageIdx: 5, startTime: "16:40", endTime: "17:20", performer: "The Roadside INN", country: "", remark: "" },
  { index: 72, dateIdx: 2, stageIdx: 5, startTime: "18:00", endTime: "18:40", performer: "LINION", country: "", remark: "" },
  { index: 73, dateIdx: 2, stageIdx: 5, startTime: "19:20", endTime: "20:00", performer: "YELLOW", country: "", remark: "" },
  { index: 74, dateIdx: 2, stageIdx: 5, startTime: "20:40", endTime: "21:20", performer: "體熊專科", country: "", remark: "" },
  { index: 75, dateIdx: 2, stageIdx: 6, startTime: "12:00", endTime: "12:40", performer: "老貓偵探社", country: "", remark: "" },
  { index: 76, dateIdx: 2, stageIdx: 6, startTime: "13:20", endTime: "14:00", performer: "DSPS", country: "", remark: "" },
  { index: 77, dateIdx: 2, stageIdx: 6, startTime: "14:40", endTime: "15:20", performer: "Who the Bitch", country: "", remark: "" },
  { index: 78, dateIdx: 2, stageIdx: 6, startTime: "16:00", endTime: "16:40", performer: "拾音", country: "", remark: "" },
  { index: 79, dateIdx: 2, stageIdx: 6, startTime: "17:20", endTime: "18:00", performer: "The vastards", country: "", remark: "" },
  { index: 80, dateIdx: 2, stageIdx: 6, startTime: "18:40", endTime: "19:20", performer: "拾亝樂團", country: "", remark: "" },
  { index: 81, dateIdx: 2, stageIdx: 6, startTime: "20:00", endTime: "20:40", performer: "OBSESS", country: "", remark: "" },
  { index: 82, dateIdx: 2, stageIdx: 6, startTime: "21:20", endTime: "22:00", performer: "皇后皮箱", country: "", remark: "" },
  { index: 83, dateIdx: 2, stageIdx: 7, startTime: "12:40", endTime: "13:20", performer: "粗大BAND", country: "", remark: "" },
  { index: 84, dateIdx: 2, stageIdx: 7, startTime: "14:00", endTime: "14:40", performer: "黑狼快速動眼那卡西", country: "", remark: "" },
  { index: 85, dateIdx: 2, stageIdx: 7, startTime: "15:20", endTime: "16:00", performer: "逆瓣膜", country: "", remark: "" },
  { index: 86, dateIdx: 2, stageIdx: 7, startTime: "16:40", endTime: "17:20", performer: "眠腦", country: "", remark: "" },
  { index: 87, dateIdx: 2, stageIdx: 7, startTime: "18:00", endTime: "18:40", performer: "Goober Gun", country: "UK", remark: "" },
  { index: 88, dateIdx: 2, stageIdx: 7, startTime: "19:20", endTime: "20:00", performer: "瑪啡因", country: "", remark: "" },
  { index: 89, dateIdx: 2, stageIdx: 7, startTime: "20:40", endTime: "21:20", performer: "Stranded Whale", country: "HK", remark: "" },
  { index: 90, dateIdx: 2, stageIdx: 8, startTime: "12:00", endTime: "12:40", performer: "感覺莓果", country: "", remark: "" },
  { index: 91, dateIdx: 2, stageIdx: 8, startTime: "13:20", endTime: "14:00", performer: "Wednesday與壞透樂團", country: "", remark: "" },
  { index: 92, dateIdx: 2, stageIdx: 8, startTime: "14:40", endTime: "15:20", performer: "昴宿", country: "", remark: "" },
  { index: 93, dateIdx: 2, stageIdx: 8, startTime: "16:00", endTime: "16:40", performer: "江東成名", country: "", remark: "" },
  { index: 94, dateIdx: 2, stageIdx: 8, startTime: "17:20", endTime: "18:00", performer: "五五身", country: "", remark: "" },
  { index: 95, dateIdx: 2, stageIdx: 8, startTime: "18:40", endTime: "19:20", performer: "YellowBlack", country: "", remark: "" },
  { index: 96, dateIdx: 2, stageIdx: 8, startTime: "20:00", endTime: "20:40", performer: "MAFANA", country: "", remark: "" },
  { index: 97, dateIdx: 2, stageIdx: 8, startTime: "21:20", endTime: "22:00", performer: "ARCPLG羣島", country: "", remark: "" },
  { index: 98, dateIdx: 2, stageIdx: 9, startTime: "14:00", endTime: "14:40", performer: "周穆", country: "", remark: "" },
  { index: 99, dateIdx: 2, stageIdx: 9, startTime: "15:20", endTime: "16:00", performer: "榕幫", country: "", remark: "" },
  { index: 100, dateIdx: 2, stageIdx: 9, startTime: "16:40", endTime: "17:20", performer: "呱吉", country: "", remark: "" },
  { index: 101, dateIdx: 2, stageIdx: 9, startTime: "18:00", endTime: "18:40", performer: "DJ Ralf", country: "", remark: "" },
  { index: 102, dateIdx: 2, stageIdx: 9, startTime: "19:20", endTime: "20:00", performer: "視網膜 & 動眼神經", country: "", remark: "" },
  { index: 103, dateIdx: 2, stageIdx: 9, startTime: "20:40", endTime: "21:20", performer: "莫宰羊", country: "", remark: "" },
  { index: 104, dateIdx: 2, stageIdx: 10, startTime: "12:40", endTime: "13:10", performer: "逆瓣膜 x 瑪啡因 Maffine", country: "", remark: "" },
  { index: 105, dateIdx: 2, stageIdx: 10, startTime: "14:00", endTime: "14:30", performer: "美秀集團 x 老王樂隊", country: "", remark: "" },
  { index: 106, dateIdx: 2, stageIdx: 10, startTime: "15:20", endTime: "15:40", performer: "優雅逆轉 x 體熊專科", country: "", remark: "" },
  { index: 107, dateIdx: 2, stageIdx: 10, startTime: "16:40", endTime: "17:10", performer: "血肉果汁機", country: "", remark: "" },
  { index: 108, dateIdx: 2, stageIdx: 10, startTime: "18:00", endTime: "18:30", performer: "拍謝少年 x  皇后皮箱", country: "", remark: "" },
  { index: 109, dateIdx: 3, stageIdx: 1, startTime: "12:40", endTime: "13:20", performer: "滅火器", country: "", remark: "" },
  { index: 110, dateIdx: 3, stageIdx: 1, startTime: "14:00", endTime: "14:40", performer: "SEX MACHINEGUNS", country: "JP", remark: "" },
  { index: 111, dateIdx: 3, stageIdx: 1, startTime: "15:20", endTime: "16:00", performer: "告五人", country: "", remark: "" },
  { index: 112, dateIdx: 3, stageIdx: 1, startTime: "16:40", endTime: "17:20", performer: "1976", country: "", remark: "" },
  { index: 113, dateIdx: 3, stageIdx: 1, startTime: "18:00", endTime: "18:40", performer: "法茲 FAZI", country: "CN", remark: "" },
  { index: 114, dateIdx: 3, stageIdx: 1, startTime: "19:20", endTime: "20:00", performer: "回聲樂團", country: "", remark: "" },
  { index: 115, dateIdx: 3, stageIdx: 1, startTime: "20:40", endTime: "21:20", performer: "土屋安娜", country: "JP", remark: "" },
  { index: 116, dateIdx: 3, stageIdx: 2, startTime: "12:00", endTime: "12:40", performer: "猛虎巧克力", country: "", remark: "" },
  { index: 117, dateIdx: 3, stageIdx: 2, startTime: "13:20", endTime: "14:00", performer: "無妄合作社", country: "", remark: "" },
  { index: 118, dateIdx: 3, stageIdx: 2, startTime: "14:40", endTime: "15:20", performer: "傷心欲絕", country: "", remark: "" },
  { index: 119, dateIdx: 3, stageIdx: 2, startTime: "16:00", endTime: "16:40", performer: "CHAI", country: "JP", remark: "" },
  { index: 120, dateIdx: 3, stageIdx: 2, startTime: "17:20", endTime: "18:00", performer: "toconoma", country: "JP", remark: "" },
  { index: 121, dateIdx: 3, stageIdx: 2, startTime: "18:40", endTime: "19:20", performer: "高嘉丰", country: "CN", remark: "" },
  { index: 122, dateIdx: 3, stageIdx: 2, startTime: "20:00", endTime: "20:40", performer: "八十八顆芭樂籽", country: "", remark: "" },
  { index: 123, dateIdx: 3, stageIdx: 2, startTime: "21:20", endTime: "22:00", performer: "Tizzy Bac", country: "", remark: "" },
  { index: 124, dateIdx: 3, stageIdx: 3, startTime: "12:40", endTime: "13:20", performer: "甜約翰", country: "", remark: "" },
  { index: 125, dateIdx: 3, stageIdx: 3, startTime: "14:00", endTime: "14:40", performer: "流氓阿德", country: "", remark: "" },
  { index: 126, dateIdx: 3, stageIdx: 3, startTime: "15:20", endTime: "16:00", performer: "I Mean Us", country: "", remark: "" },
  { index: 127, dateIdx: 3, stageIdx: 3, startTime: "16:40", endTime: "17:20", performer: "風籟坊 Windmill", country: "", remark: "" },
  { index: 128, dateIdx: 3, stageIdx: 3, startTime: "18:00", endTime: "18:40", performer: "P!SCO", country: "", remark: "" },
  { index: 129, dateIdx: 3, stageIdx: 3, startTime: "19:20", endTime: "20:00", performer: "恕", country: "", remark: "" },
  { index: 130, dateIdx: 3, stageIdx: 3, startTime: "20:40", endTime: "21:20", performer: "火燒島", country: "", remark: "" },
  { index: 131, dateIdx: 3, stageIdx: 4, startTime: "12:00", endTime: "12:40", performer: "dela", country: "JP", remark: "" },
  { index: 132, dateIdx: 3, stageIdx: 4, startTime: "13:20", endTime: "14:00", performer: "凹與山", country: "", remark: "" },
  { index: 133, dateIdx: 3, stageIdx: 4, startTime: "14:40", endTime: "15:20", performer: "KoOk", country: "", remark: "" },
  { index: 134, dateIdx: 3, stageIdx: 4, startTime: "16:00", endTime: "16:40", performer: "南瓜妮歌迷俱樂部", country: "", remark: "" },
  { index: 135, dateIdx: 3, stageIdx: 4, startTime: "17:20", endTime: "18:00", performer: "FLUX", country: "", remark: "" },
  { index: 136, dateIdx: 3, stageIdx: 4, startTime: "18:40", endTime: "19:20", performer: "晨曦光廊", country: "", remark: "" },
  { index: 137, dateIdx: 3, stageIdx: 4, startTime: "20:00", endTime: "20:40", performer: "Maniac", country: "HK", remark: "" },
  { index: 138, dateIdx: 3, stageIdx: 4, startTime: "21:20", endTime: "22:00", performer: "鄭興", country: "CN", remark: "" },
  { index: 139, dateIdx: 3, stageIdx: 5, startTime: "11:20", endTime: "11:50", performer: "王淯騰", country: "", remark: "" },
  { index: 140, dateIdx: 3, stageIdx: 5, startTime: "12:10", endTime: "12:40", performer: "WARM WALL 鄧志峰 & 暖巢", country: "MO", remark: "" },
  { index: 141, dateIdx: 3, stageIdx: 5, startTime: "13:20", endTime: "14:00", performer: "地下道樂團", country: "", remark: "" },
  { index: 142, dateIdx: 3, stageIdx: 5, startTime: "14:40", endTime: "15:20", performer: "熱寫生", country: "", remark: "" },
  { index: 143, dateIdx: 3, stageIdx: 5, startTime: "16:00", endTime: "16:40", performer: "The Tic Tac", country: "", remark: "" },
  { index: 144, dateIdx: 3, stageIdx: 5, startTime: "17:20", endTime: "18:00", performer: "厭世少年", country: "", remark: "" },
  { index: 145, dateIdx: 3, stageIdx: 5, startTime: "18:40", endTime: "19:20", performer: "神棍樂團", country: "", remark: "" },
  { index: 146, dateIdx: 3, stageIdx: 5, startTime: "20:00", endTime: "20:40", performer: "魏嘉瑩 & Arrow Band", country: "", remark: "" },
  { index: 147, dateIdx: 3, stageIdx: 5, startTime: "21:20", endTime: "22:00", performer: "The eXtensions", country: "", remark: "" },
  { index: 148, dateIdx: 3, stageIdx: 6, startTime: "12:40", endTime: "13:20", performer: "Rappelkopf", country: "KR", remark: "" },
  { index: 149, dateIdx: 3, stageIdx: 6, startTime: "14:00", endTime: "14:40", performer: "SHOOT UP", country: "", remark: "" },
  { index: 150, dateIdx: 3, stageIdx: 6, startTime: "15:20", endTime: "16:00", performer: "KINEMAS", country: "JP", remark: "" },
  { index: 151, dateIdx: 3, stageIdx: 6, startTime: "16:40", endTime: "17:20", performer: "Empty ORio ft.異鄉人", country: "", remark: "" },
  { index: 152, dateIdx: 3, stageIdx: 6, startTime: "18:00", endTime: "18:40", performer: "Greedy Black Hole", country: "", remark: "" },
  { index: 153, dateIdx: 3, stageIdx: 6, startTime: "19:20", endTime: "20:00", performer: "迷幻雪芒果", country: "MY", remark: "" },
  { index: 154, dateIdx: 3, stageIdx: 6, startTime: "20:40", endTime: "21:20", performer: "LOKA", country: "JP", remark: "" },
  { index: 155, dateIdx: 3, stageIdx: 7, startTime: "12:00", endTime: "12:40", performer: "逃走鮑伯", country: "", remark: "" },
  { index: 156, dateIdx: 3, stageIdx: 7, startTime: "13:20", endTime: "14:00", performer: "黎可辰", country: "", remark: "" },
  { index: 157, dateIdx: 3, stageIdx: 7, startTime: "14:40", endTime: "15:20", performer: "暴君", country: "", remark: "" },
  { index: 158, dateIdx: 3, stageIdx: 7, startTime: "16:00", endTime: "16:40", performer: "倒車入庫", country: "", remark: "" },
  { index: 159, dateIdx: 3, stageIdx: 7, startTime: "17:20", endTime: "18:00", performer: "變胎", country: "", remark: "" },
  { index: 160, dateIdx: 3, stageIdx: 7, startTime: "18:40", endTime: "19:20", performer: "共犯結構", country: "", remark: "" },
  { index: 161, dateIdx: 3, stageIdx: 7, startTime: "20:00", endTime: "20:40", performer: "SUBLIMITY", country: "JP", remark: "" },
  { index: 162, dateIdx: 3, stageIdx: 7, startTime: "21:20", endTime: "22:00", performer: "煙雨飄渺", country: "", remark: "" },
  { index: 163, dateIdx: 3, stageIdx: 8, startTime: "12:40", endTime: "13:20", performer: "皮格子", country: "", remark: "" },
  { index: 164, dateIdx: 3, stageIdx: 8, startTime: "14:00", endTime: "14:40", performer: "錦安", country: "SG", remark: "" },
  { index: 165, dateIdx: 3, stageIdx: 8, startTime: "15:20", endTime: "16:00", performer: "The Sulis Club", country: "HK", remark: "" },
  { index: 166, dateIdx: 3, stageIdx: 8, startTime: "16:40", endTime: "17:20", performer: "理想混蛋 Bestards", country: "", remark: "" },
  { index: 167, dateIdx: 3, stageIdx: 8, startTime: "18:00", endTime: "18:40", performer: "12.8 Twelve.eight", country: "HK", remark: "" },
  { index: 168, dateIdx: 3, stageIdx: 8, startTime: "19:20", endTime: "20:00", performer: "記號士", country: "", remark: "" },
  { index: 169, dateIdx: 3, stageIdx: 8, startTime: "20:40", endTime: "21:20", performer: "神奇膠", country: "HK", remark: "" },
  { index: 170, dateIdx: 3, stageIdx: 9, startTime: "14:40", endTime: "15:20", performer: "王水源 H2O", country: "", remark: "" },
  { index: 171, dateIdx: 3, stageIdx: 9, startTime: "16:00", endTime: "16:40", performer: "臭屁嬰仔", country: "", remark: "" },
  { index: 172, dateIdx: 3, stageIdx: 9, startTime: "17:20", endTime: "18:00", performer: "拷秋勤 EX", country: "", remark: "" },
  { index: 173, dateIdx: 3, stageIdx: 9, startTime: "18:40", endTime: "19:20", performer: "裸繪札", country: "JP", remark: "" },
  { index: 174, dateIdx: 3, stageIdx: 9, startTime: "20:00", endTime: "20:40", performer: "DJ 陳玠安", country: "", remark: "" },
  { index: 175, dateIdx: 3, stageIdx: 9, startTime: "21:20", endTime: "22:00", performer: "阿舌", country: "", remark: "" },
  { index: 176, dateIdx: 3, stageIdx: 10, startTime: "12:10", endTime: "12:40", performer: "異鄉人 x 晨曦光廊", country: "MO", remark: "" },
  { index: 177, dateIdx: 3, stageIdx: 10, startTime: "13:20", endTime: "14:00", performer: "滅火器", country: "", remark: "" },
  { index: 178, dateIdx: 3, stageIdx: 10, startTime: "14:40", endTime: "15:10", performer: "猛虎巧克力 x 五五身", country: "", remark: "" },
  { index: 179, dateIdx: 3, stageIdx: 10, startTime: "16:00", endTime: "16:30", performer: "P!SCO X FLUX", country: "", remark: "" },
  { index: 180, dateIdx: 3, stageIdx: 10, startTime: "17:20", endTime: "17:40", performer: "火燒島 x 八十八顆芭樂籽", country: "", remark: "" },
];

let eventRef = db.ref("events");

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
  firebase:{
    eventRef
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
