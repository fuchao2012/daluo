<template>
  <div class="demo-mint-ui">
    <mt-header title="标题过长会隐藏后面的内容啊哈哈哈哈">
      <router-link to="/" slot="left">
        <mt-button icon="back">返回</mt-button>
      </router-link>
      <mt-button icon="more" slot="right"></mt-button>
    </mt-header>

    <mt-field label="用户名" placeholder="请输入用户名" v-model="username"></mt-field>
    <mt-field label="邮箱" placeholder="请输入邮箱" type="email" v-model="email"></mt-field>
    <mt-field label="密码" placeholder="请输入密码" type="password" v-model="password"></mt-field>
    <mt-field label="手机号" placeholder="请输入手机号" type="tel" v-model="phone"></mt-field>
    <mt-field label="网站" placeholder="请输入网址" type="url" v-model="website"></mt-field>
    <mt-field label="数字" placeholder="请输入数字" type="number" v-model="number"></mt-field>
    <mt-field label="生日" placeholder="请输入生日" type="date" v-model="birthday"></mt-field>
    <mt-field label="自我介绍" placeholder="自我介绍" type="textarea" rows="4" v-model="introduction"></mt-field>
    <mt-checklist
      title="复选框列表"
      v-model="checkListValue"
      :options="['选项A', '选项B', '选项C']">
    </mt-checklist>
    <mt-cell title="标题文字" value="说明文字"></mt-cell>
    <mt-cell
      title="标题文字"
      to="//github.com"
      is-link
      value="带链接">
    </mt-cell>
    <mt-range :value.sync="rangeValue">
      <div slot="start">0</div>
      <div slot="end">100</div>
    </mt-range>
    <mt-range
      :value.sync="rangeValue"
      :min="10"
      :max="90"
      :step="10"
      :bar-height="5">
    </mt-range>
    <mt-datetime-picker
      :visible.sync="pickerVisible"
      :value.sync="pickerValue"
      type="date"
      year-format="{value} 年"
      month-format="{value} 月"
      date-format="{value} 日">
    </mt-datetime-picker>
    <mt-search
      v-model="value"
      cancel-text="取消"
      placeholder="搜索">
    </mt-search>
    <mt-button>
      <mt-spinner type="fading-circle" slot="icon"></mt-spinner>
    </mt-button>
    <mt-switch v-model="switchValue"></mt-switch>
    <mt-progress :value="20" :bar-height="5"></mt-progress>
    <mt-picker :slots="slots" @change="pickerChange"></mt-picker>
    <mt-button type="danger" @click.native="handleButtonClick">Hello Toast</mt-button>
    <mt-button type="danger" @click.native="pickerVisible=!pickerVisible">Hello picker</mt-button>
    <mt-button type="danger" @click.native="handleIndicatorClick">Hello Indicator</mt-button>
    <mt-button type="danger" @click.native="handleMessageBoxClick">Hello MessageBox</mt-button>
    <mt-button type="danger" @click.native="handleActionsheetClick">Hello Actionsheet</mt-button>
    <mt-button type="danger" @click.native="popUp">Hello popUp</mt-button>
    <mt-button icon="more">更多</mt-button>
    <mt-badge type="warning" size="small">30</mt-badge>
    <mt-badge size="normal">10</mt-badge>
    <mt-badge size="large">10</mt-badge>
    <!--<mt-loadmore :top-method="loadTop" :bottom-method="loadBottom" :bottom-all-loaded="allLoaded" ref="loadmore">-->
    <!--<ul>-->
    <!--<li v-for="item in list">{{ item }}</li>-->
    <!--</ul>-->
    <!--</mt-loadmore>-->

    <!--<ul-->
    <!--v-infinite-scroll="loadMore"-->
    <!--infinite-scroll-disabled="loading"-->
    <!--infinite-scroll-distance="10">-->
    <!--<li v-for="item in list">{{ item }}</li>-->
    <!--</ul>-->
    <mt-actionsheet
      :actions="actions"
      :visible.sync="sheetVisible">
    </mt-actionsheet>
    <mt-popup
      :visible.sync="popupVisible"
      popup-transition="popup-fade"
      position="bottom"
    >
      Hello
    </mt-popup>
    <mt-swipe :auto="4000" :show-indicators="false" class="swipe-container">
      <mt-swipe-item>1</mt-swipe-item>
      <mt-swipe-item>2</mt-swipe-item>
      <mt-swipe-item>3</mt-swipe-item>
    </mt-swipe>

    <mt-navbar v-model="selected">
      <mt-tab-item id="11">选项一</mt-tab-item>
      <mt-tab-item id="22">选项二</mt-tab-item>
      <mt-tab-item id="33">选项三</mt-tab-item>
    </mt-navbar>

    <!-- tab-container -->
    <mt-tab-container v-model="selected">
      <mt-tab-container-item id="1">
        <mt-cell v-for="n in 6" :title="'内容 ' + n"></mt-cell>
      </mt-tab-container-item>
      <mt-tab-container-item id="2">
        <mt-cell v-for="n in 4" :title="'测试 ' + n"></mt-cell>
      </mt-tab-container-item>
      <mt-tab-container-item id="3">
        <mt-cell v-for="n in 6" :title="'选项 ' + n"></mt-cell>
      </mt-tab-container-item>
    </mt-tab-container>
    <mt-tabbar v-model="selected">
      <mt-tab-item id="外卖">
        <img slot="icon" src="">
        外卖
      </mt-tab-item>
      <mt-tab-item id="订单">
        <img slot="icon" src="">
        订单
      </mt-tab-item>
      <mt-tab-item id="发现">
        <img slot="icon" src="">
        发现
      </mt-tab-item>
      <mt-tab-item id="我的">
        <img slot="icon" src="">
        我的
      </mt-tab-item>
    </mt-tabbar>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
        allLoaded: false,
        list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
        loading: true,
        checkListValue: [],
        rangeValue: 20,
        switchValue: true,
        selected: '订单',
        value: 'abc',
        username: '',
        email: '',
        password: '',
        phone: '',
        website: '',
        number: '',
        birthday: '',
        introduction: '',
        actions: [{
          name: 'hello',
          method(){
            console.log('hello')
          }
        }, {
          name: 'hello2',
          method(){
            console.log('hello2')
          }
        }, {
          name: 'hello3',
          method(){
            console.log('hello3')
          }
        }],
        sheetVisible: true,
        popupVisible: true,
        pickerVisible: true,
        pickerValue: '',
        slots: [
          {
            flex: 1,
            values: ['2015-01', '2015-02', '2015-03', '2015-04', '2015-05', '2015-06'],
            className: 'slot1',
            textAlign: 'right'
          }, {
            divider: true,
            content: '-',
            className: 'slot2'
          }, {
            flex: 1,
            values: ['2015-01', '2015-02', '2015-03', '2015-04', '2015-05', '2015-06'],
            className: 'slot3',
            textAlign: 'left'
          }
        ]
      }
    },
    computed: {
      handleButtonClick: function () {
        this.$toast({
          message: '提示',
          position: 'bottom',
          duration: 5000,
          iconClass: 'icon icon-success'
        })
      },
      handleIndicatorClick: function () {
        this.$indicator.open({
          text: '加载中...',
          spinnerType: 'fading-circle'
        })
      },
      handleMessageBoxClick: function () {
        this.$messagebox({
          title: '提示',
          message: '确定执行此操作?',
          showCancelButton: true
        })
      }
    },
    methods: {
      pickerChange: function (picker, values) {
        if (values[0] > values[1]) {
          picker.setSlotValue(1, values[0])
        }
      },
      popUp: function () {
        this.popupVisible = !this.popupVisible
      },
      handleActionsheetClick: function () {
        this.sheetVisible = !this.sheetVisible
      },
      loadTop: function () {
        this.$refs.loadmore.onTopLoaded()
      },
      loadBottom: function () {
        this.allLoaded = true;
        this.$refs.loadmore.onBottomLoaded()
      },
      loadMore() {
        this.loading = true;
        setTimeout(() => {
          let last = this.list[this.list.length - 1];
          for (let i = 1; i <= 10; i++) {
            this.list.push(last + i)
          }
          this.loading = false
        }, 2500)
      }
    }

  }
</script>
<style>
  .swipe-container {
    width: 100%;
    height: 200px;
  }
</style>
