<template>
  <div>
    
    <div class="center-card-right bg-image card-shadow">
      <span @click="toggleCountySelect">{{countyValue}}</span>
      <ul v-if="showCountyOption">
        <li v-for="item in countyOption"
            :key="item.value"
            :label="item.label"
            :value="item.index"
            @click="selectCounty(item)">{{item.label}}
        </li>
      </ul>
    </div>
    <SvgDetail :selectedArea="countyValue"
               :countyOption="countyOption"
               @svgChangeArea="svgChangeArea"></SvgDetail>
  </div>
</template>

<script>
import SvgDetail from './lib/SvgDetail'
export default {
  components: { SvgDetail },
  name: 'Page404',
  computed: {
    message () {
      return 'The webmaster said that you can not enter this page...'
    }
  },
  data () {
    return {
      showCountyOption: false,
      countyOption: [{
        value: '0',
        label: '东江流域'
      }, {
        value: '4402',
        index:'1',
        label: '韶关'
      }, {
        value: '4403',
        index:'2',
        label: '深圳'
      }, {
        value: '4413',
        index:'3',
        label: '惠州'
      }, {
        value: '4419',
        index:'4',
        label: '东莞'
      }, {
        value: '4401',
        index:'5',
        label: '广州'
      }, {
        value: '4416',
        index:'6',
        label: '河源'
      }],
      countyValue: '东江流域'
    }
  },
  methods: {
    toggleCountySelect () {
      this.showCountyOption = !this.showCountyOption
    },
    selectCounty(item){
      this.countyValue=item.label
      this.showCountyOption = !this.showCountyOption
      this.$emit('select-county',item)
    },
    svgChangeArea(index){
      let item=_.find(this.countyOption,{index})
      this.countyValue=item.label
      this.$emit('county-change',item)
    }
  }
}
</script>

<style lang="scss" scoped>
$fontColor: #00fcf9;
.center-card-right {
  width: 7rem;
  height: 2.5rem;
  line-height: 2.5rem;
  position: absolute;
  left: 1rem;
  top: 1rem;
  z-index: 12;
  color: $fontColor;
  text-align: center;
  background-image: url("~@/assets/images/sumary/base/center-card-right.png");
  span {
    font-size: 1rem;
  }
  ul,li{
    padding: 0;
    margin: 0;
    list-style: none;
    font-style: normal;
    text-decoration: none;
    border: none;
    font-family: Microsoft Yahei,sans-serif;
    -webkit-tap-highlight-color: transparent;
    -webkit-font-smoothing: antialiased;
  }
  ul {
    background: #053f6163;
    li{
      user-select: none;
    cursor: pointer;
    }
    li:hover {
      background-position: 6px;
      background-repeat: no-repeat;
      background-image: url("~@/assets/images/sumary/base/center-card-right.png");
      background-size: calc(100% - 12px) 100%;
    }
  }
}
.bg-image {
  background-repeat: no-repeat;
  background-size: 100% 100%;
}
.card-shadow:hover {
  box-shadow: 0 0 4px #fff;
  cursor: pointer;
}
</style>
