<template>
  <section  id="app">
      <div id="head">
        <img src="./assets/bg.jpg" >
      </div>
      <article>
        <div id="table">
          <div class="ranker" id="ranker">
            <div class="rank-level">名次</div>
            <div class="player-server">区服</div>
            <div class="player-name">角色名</div>
            <div class="pre-get">领取条件</div>
          </div>
          
          <div class="ranker" v-for="data in dataList">
            <div class="rank-level">{{data.rank}}</div>
            <div class="player-server">{{data.server}}区</div>
            <div class="player-name">{{data.playerName}}</div>
            <div class="pre-get">{{data.get}}</div>
          </div>
        </div>
         <aside>
            <h2>说明</h2>
            <p>1、本排行以活动期间角色累计充值进行排名（金额相同时充值时间靠前者排名靠前）；</p>
            <p>2、活动期间（12月28日—12月31日），排行榜上累积充值大于30000元的玩家才能获取排名奖励，低于30000元无法领取；</p>
            <p>活动结束后，榜上玩家可于5个工作日内联系工作人员领取相应奖励（奖励详见活动内容）；</p>
            <p>4、排行榜每天10点，14点，18点，22点更新；</p>
          </aside>
      </article>
     
  </section>

</template>

<script>
    export default {
        name: 'app',
        data() {
            return {
                dataList: [{
                    rank: 1,
                    server: 1,
                    playerName: '小胖',
                    get: "已达成"
                }, {
                    rank: 2,
                    server: 1,
                    playerName: '小胖',
                    get: "已达成"
                }, {
                    rank: 3,
                    server: 1,
                    playerName: '小胖',
                    get: "已达成"
                }, {
                    rank: 4,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, {
                    rank: 5,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, {
                    rank: 6,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, {
                    rank: 7,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, {
                    rank: 8,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, {
                    rank: 9,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, {
                    rank: 10,
                    server: 1,
                    playerName: '小胖',
                    get: "未达成"
                }, ]
            }
        }
    }
</script>

<style lang="sass">
    @import './assets/index.scss';
</style>