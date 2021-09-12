<template>
  <div class="hello">
    <h1>TTT(Talk Theme Tune)</h1>
    <p>
      トークテーマを決定します。
    </p>
    <button @click="tune">チューン！</button>
    <ul>
      <li v-for="(value, key) in talkThemeList" :class="{tuned:value.tuned}" :key="key">
        {{ value.talkTheme }}
      </li>
    </ul>
  </div>
</template>

<script>
import talkTheme from '../assets/talkTheme.json';

export default {
  name: 'TalkThemeTune',
  props: {
    msg: String
  },
  data() {
    return {
      talkThemeList: talkTheme.talkThemeList
    }
  },
  methods: {
    tune: function(){
      const self = this;
      let counter = 0;
      let targetIndex = 0;
      let timerID = setInterval(() => {
        counter++;
        if (counter == 30) {
          clearInterval(timerID);
        }
        // 初期化
        for (let i in self.talkThemeList) {
          self.talkThemeList[i].tuned = false;
        }
        // ランダムに選択
        targetIndex = Math.floor(Math.random() * self.talkThemeList.length);
        self.talkThemeList[targetIndex].tuned = true;
      }, 100)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul, ol {
  padding: 0;
  position: relative;
}
ul li, ol li {
  color: #2d8fdd;
  border-left: solid 6px #2d8fdd;/*左側の線*/
  background: #f1f8ff;/*背景色*/
  margin-bottom: 3px;/*下のバーとの余白*/
   line-height: 1.5;
  padding: 0.5em;
  list-style-type: none!important;/*ポチ消す*/
}
.tuned {
  background: #ffeaea;
  box-shadow: 0px 0px 0px 10px #ffeaea;
  border: dashed 2px #ffc3c3;
  border-left: solid 6px #2d8fdd;/*左側の線*/
  /* border-radius: 8px; */
  margin-bottom: 3px;/*下のバーとの余白*/
   line-height: 1.5;
  padding: 0.5em;
  list-style-type: none!important;/*ポチ消す*/
  animation: flash 1s linear 5;
}

@keyframes flash {
  0%,100% {
    opacity: 1;
  }

  50% {
    opacity: 0;
  }
}
</style>
