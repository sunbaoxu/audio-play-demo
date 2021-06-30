<template>
  <div class="home-wrap">
    这是audio的demo页面
    <!-- controls -->
    <audio ref="audioId" src="~@/assets/back.mp3" loop ></audio>
    <audio ref="errorId" src="~@/assets/error.mp3"></audio>
    <audio ref="successId" src="~@/assets/success.mp3"></audio>
    <button @click="successFn">成功音效</button>
    <button @click="errorFn">失败音效</button>
    <button @click="async = true">设置音量</button>
    <mt-popup v-model="async">
      <section class="volume-box">
        <div class="ul">
          <div class="li">
            <p class="name">背景音量</p>
            <mt-range v-model="backValue" class="val"></mt-range>
          </div>
          <div class="li">
            <p class="name">音效音量</p>
            <mt-range v-model="effectValue" class="val"></mt-range>
          </div>
        </div>
      </section>
    </mt-popup>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      backValue: 100,
      effectValue: 100,
      async: false
    }
  },
  watch :{
    backValue (val) {
      this.$refs.audioId.volume = val / 100
      console.log(val / 100)
    },
    effectValue (val) {
      this.$refs.successId.volume = val / 100
      this.$refs.errorId.volume = val / 100
    }
  },
  methods: {
    successFn(){
      this.$refs.successId.play();//点击触发 点击音效
    },
    errorFn(){
      this.$refs.errorId.play();//点击触发 点击音效
    }
  },
  mounted () {
	  // 播放音乐
    this.$refs.audioId.play()
    console.log(this.$refs.audioId)
    this.$refs.audioId.onended = () =>{
      this.$refs.audioId.load();
      // this.$refs.audioId.play();
    }
  }
}
</script>
<style lang="scss" scoped>
.home-wrap{
  .volume-box{
    width: 300px;
    padding: 0 30px;
    .li{
      display: flex;
      height: 80px;
      align-items: center;
      .name{
        width: 100px;
      }
      .val{
        flex: 1;
      }
    }
  }
}
</style>
