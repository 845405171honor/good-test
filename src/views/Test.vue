<template>
  <div class="test">
    <div>
      平均值: {{average}}
    </div>
    <button @click="update">加载更多</button>
    <div v-for="item in dataList" :key="item.id">
      <div class="list">
        <div>{{item.id}}</div>
        <div>{{item.data}}</div>
      </div>
      <div style="text-align:center">{{item.time}}</div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'test',
  data () {
    return {
      dataList: [],
      average: ''
    }
  },
  created () {
    this.good()
  },
  computed: {

  },
  methods: {
    update () {
      this.good()
    },
    good () {
      let sum = 0
      this.$store.dispatch('getDataCall').then((res) => {
        this.$store.state.dataList = res
        this.dataList = res
        for (let i = 0; i < res.length; i++) {
          sum += res[i].data
          this.average = (sum / res.length).toFixed(2)
        }
      })
    }

  }
}
</script>

<style scoped lang="less">

.test{

  .list{
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
  button{
    margin-top: 10px;
    margin-bottom: 10px;
    background-color: blue;
    padding: 10px;
    font-size: 15px;
    color: white;
    width: 100%;
  }
}

</style>
