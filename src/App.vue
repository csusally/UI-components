<template>
  <div id="app">
    <!-- search-bar -->
    <h2 class="title">search-bar</h2>
    <search-bar></search-bar>

    <!-- 滑动 -->
    <h2 class="title">slider</h2>
    <Slider :imgList="imgList" sty="-webkit-animation-duration:16s;"></Slider>

    <!-- Dialog 對話框 -->
    <Dialog v-show="dialogControl" type="confirm" title="弹框标题哦" confirmTextColor='red' 
      @weui-dialog-confirm="handleDialogAction(1)"
      @weui-dialog-cancel="handleDialogAction(0)"> 
      {{dialogContent}}
    </Dialog>

    <!-- Modal 彈框 与 对话框类似 -->
    <Modal :modalData = 'modalData' :showModal='showModal'></Modal>

    <!-- toast 提示框 一定时间后消失-->
    <h2 class="title">toast 提示框</h2>
    <button @click="showToast">showtoast 2秒消失</button>
    <button @click="toastshow">showtoast</button>
    <button @click="toasthide">hidetoast </button>

    <h2 class="title">load-more</h2>
    <button>加载数据</button>
    <load-more></load-more>

    <!-- picker -->
    <h2 class="title">picker</h2>
    <button @click="showpicker">picker show</button>
    <span v-if="dialogItem" style='color:orange;margin-left:20px;'>您的选择为{{dialogItem.label}}</span>
    <picker ref="picker" @selectItem='selectedItem'></picker>


    <h2 class="title">switch</h2>
    <switch-input></switch-input>

    <h2 class="title">check</h2>
    <check checktype='checkbox'></check>
    <text-input></text-input>
  </div>
</template>

<script>
import Slider from "./components/slider-simple/slider-simple";
import SearchBar from "./components/search-bar/search-bar";
import LoadMore from "./components/load-more/load-more";
import Picker from "./components/picker/picker";
import SwitchInput from "./components/input/switch/switchInput";
import check from "./components/input/check/check";
import TextInput from "./components/input/textinput/textinput";
export default {
  name: 'app',
  data () {
    return {
      dialogControl: false,
      dialogContent: '',
      dialogItem:'',
      isShowToast: false,
      imgList: ['http://img5.imgtn.bdimg.com/it/u=2198746125,2255961738&fm=26&gp=0.jpg',
      'http://img.zcool.cn/community/01f09e577b85450000012e7e182cf0.jpg@1280w_1l_2o_100sh.jpg',
      'http://pic19.nipic.com/20120308/4970979_102637717125_2.jpg'
      ],
      modalData:{
        confirmText:'确定',
        cancelText:'取消',
        content: 'dsfdasfasdgfdsgsgdfgdf?',
        confirmColor: 'green',
        confirmFun: ()=>{
          // this.confirm();
          this.showModal = false;
        },
        cancelFun: ()=>{
          console.log('cancel')
          this.showModal = false;
        }
      },
      showModal: false
    }
  },
  mounted(){
  },
  methods: {
    handleDialogAction (action) {
      // alert(`你刚刚点击了“${action}”`)
      this.dialogControl = false
    },
    showToast(){
      this.$toast('我是弹出消息')
    },
    toastshow(){
      this.$showToast('show我是弹出消息我是弹出消息');
      // setTimeout(() => {
      //   this.toasthide();
      // }, 4000);
    },
    toasthide(){
      this.$hideToast()
    },
    showpicker(){
      this.$refs.picker._data.isShow = true;
    },
    selectedItem(param){
      this.dialogControl = true;
      this.dialogItem = param;
      this.dialogContent = `你确定要选择${param.label}吗?`;
      console.log(param.label)
    }
  },
  components: {
    Slider,
    SearchBar,
    LoadMore,
    Picker,
    SwitchInput,
    check,
    TextInput
  }
}
</script>

<style lang="scss">
  @import './style/base/reset';
</style>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  min-width:360px;
  padding: 20px;
}

h1, h2 {
  font-weight: normal;
}

h2.title {
  margin-top: 50px;
  text-align: left;
  color: #42b983;
  padding: 0 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.show{
  transform: translate(0, 0);
}

.hide{
  transform: translate(0, 100%);
}
</style>
