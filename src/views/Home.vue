<!-- 首页组件-->
<template>
  <div class="home" id="home" name="home">
    <!-- 轮播图END -->
    <div class="main-box">
      <div class="main" v-for="(item,index) in applianceList" :key="item.id">
        <div class="phone">
          <div class="box-hd">
            <div class="title">{{ item.typeName }}</div>
          </div>
          <div class="box-bd">
            <div class="promo-list">
              <router-link to v-if="phoneList[index]">
   <img :src="require(`../assets${phoneList[index].value}`)"/>
              <!--               <img style="height:100%;width:100%;" src="../assets/imgs/shu.webp"/>-->
              </router-link>
            </div>
            <div class="list">
              <MyList :list="item.goodsList" :isMore="true"></MyList>
            </div>
          </div>
        </div>
        <!-- 手机商品展示区域END -->
      </div>
    </div>
  </div>
</template>
<script>




export default {
  components: { },
  data() {
    return {
     
      phoneList: "", // 手机商品列表
      miTvList: "", // 小米电视商品列表
      applianceList: [], // 家电商品列表
      applianceHotList: "", //热门家电商品列表
      accessoryList: "", //配件商品列表
      accessoryHotList: "", //热门配件商品列表
      protectingShellList: "", // 保护套商品列表
      chargerList: "", //充电器商品列表
      applianceActive: 1, // 家电当前选中的商品分类
      accessoryActive: 1, // 配件当前选中的商品分类
    };
  },
  watch: {
    // 家电当前选中的商品分类，响应不同的商品数据
    applianceActive: function (val) {
      // 页面初始化的时候把applianceHotList(热门家电商品列表)直接赋值给applianceList(家电商品列表)
      // 所以在切换商品列表时判断applianceHotList是否为空,为空则是第一次切换,把applianceList赋值给applianceHotList
      if (this.applianceHotList == "") {
        this.applianceHotList = this.applianceList;
      }
      if (val == 1) {
 
        this.applianceList = this.applianceHotList;
        return;
      }
      if (val == 2) {
    
        this.applianceList = this.miTvList;
        return;
      }
    },
    accessoryActive: function (val) {
      if (this.accessoryHotList == "") {
        this.accessoryHotList = this.accessoryList;
      }
      if (val == 1) {
        
        this.accessoryList = this.accessoryHotList;
        return;
      }
      if (val == 2) {
        this.accessoryList = this.protectingShellList;
        return;
      }
      if (val == 3) {
        this.accessoryList = this.chargerList;
        return;
      }
    }
  },
  created() {
    this.getPromo()
  },
  methods: {


    // 获取各类商品数据方法封装
    getPromo() {
            this.applianceList = [
  {
    "id": "1636246470664736770",
    "typeName": "手机",
    "imgType": "电子商品类",
    "status": 1,
    "sort": 600,
    "isHome": 1,
    "createTime": "2024-01-31 16:39:59",
    "goodsList": [
      {
        "id": "1729114563303923714",
        "goodsName": "Xiaomi 14 Pro",
        "goodsPayType": 1,
        "goodsAmount": 20,
        "goodsPrice": 4999,
        "goodsDiscount": 3999,
        "goodsTypeCode": "1636246470664736770",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "Xiaomi 14 全面跨越式升级\n\n6.36″黄金尺寸，极窄视觉四等边屏幕。\n全新升级徕卡光学Summilux镜头，超大光圈，画面更加通透明亮。\n定制光影猎人900 高动态影像传感器，带来13.5EV超动态范围。\n第三代骁龙8移动平台，全新架构，能效大飞跃。\n更搭载全新小米澎湃OS，以人为中心，\n打造「人车家全生态」操作系统，将体验推进到全新高度。",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": 1,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1729114563303923714/7b12f13b4d7b48fc8a3e879ad7d2248820231127.png",
        "imgUrlList": null
      },
      {
        "id": "1636247425896501250",
        "goodsName": "OPPO 一加 Ace 2",
        "goodsPayType": 1,
        "goodsAmount": 97,
        "goodsPrice": 10000,
        "goodsDiscount": 3600,
        "goodsTypeCode": "1636246470664736770",
        "status": 1,
        "goodsOrigin": "1",
        "goodsAddress": "OPPO 一加 Ace 2 满血版骁龙®8+旗舰平台 1.5K灵犀触控屏",
        "goodsMarkCode": "2",
        "createTime": "2024-01-31 16:39:59",
        "sort": 200,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636247425896501250/47ccc9c9b0234e728603d3868c11aebd20230316.jpg",
        "imgUrlList": null
      },
      {
        "id": "1636247822233063425",
        "goodsName": "新款星盖世X13Pro",
        "goodsPayType": 1,
        "goodsAmount": 109,
        "goodsPrice": 1999,
        "goodsDiscount": 122,
        "goodsTypeCode": "1636246470664736770",
        "status": 1,
        "goodsOrigin": "1",
        "goodsAddress": "新款星盖世X13Pro真八核超薄智能手机可用5G移动联通电信卡4g全网通",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": 200,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636247822233063425/d089194c32c74ca49620991968288b9120230316.jpg",
        "imgUrlList": null
      },
      {
        "id": "1636248156569423873",
        "goodsName": "OPPO K10x 极光 8GB+128GB",
        "goodsPayType": 1,
        "goodsAmount": 1109,
        "goodsPrice": 11111,
        "goodsDiscount": 111,
        "goodsTypeCode": "1636246470664736770",
        "status": 1,
        "goodsOrigin": "111",
        "goodsAddress": "OPPO K10x 极光 8GB+128GB 67W超级闪充 5000mAh长续航 120Hz高帧屏 6400",
        "goodsMarkCode": "2",
        "createTime": "2024-01-31 16:39:59",
        "sort": 200,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636248156569423873/1fcdc194b3834edf890bf5b0f6eafea920230316.jpg",
        "imgUrlList": null
      },
      {
        "id": "1729123486555582466",
        "goodsName": "Redmi Note 13 5G",
        "goodsPayType": 1,
        "goodsAmount": 100,
        "goodsPrice": 1199,
        "goodsDiscount": 1099,
        "goodsTypeCode": "1636246470664736770",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "新 2 亿像素，更快更清晰\n中端影像新高度\n新 Note，新影像！搭载三星 HP3 旗舰传感器，1/1.4\" 大底，\nf/1.65 大光圈，支持 2 亿像素大片超清直出，单张照片分\n辨率高达 16320 x 12240。还有 OIS+EIS 双防抖和 \n2X&4X 无损变焦技术加持，将 2 亿像素清晰度、画质再\n度提升一个等级！",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": 2,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1729123486555582466/30950c4fd26f455a9d3354309b6cb1fd20231127.png",
        "imgUrlList": null
      }
    ]
  },
  {
    "id": "1729001353678553089",
    "typeName": "笔记本|平板",
    "imgType": "笔记本|平板",
    "status": 1,
    "sort": 450,
    "isHome": 1,
    "createTime": "2024-01-31 16:39:59",
    "goodsList": [
      {
        "id": "1729130169499635714",
        "goodsName": "Xiaomi Pad 6 Pro",
        "goodsPayType": 1,
        "goodsAmount": 200,
        "goodsPrice": 2499,
        "goodsDiscount": 2499,
        "goodsTypeCode": "1729001353678553089",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "强大的骁龙8+处理器\n为「生产力」提供强劲动力\n11英寸2.8K超高清屏，让你大展实力与创意\n更有专为大屏定制的MIUI Pad 14\n为你灵活掌控多种使用场景\n这一次，强上加强\n助你时刻尽兴而为，全力成事",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": null,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1729001353678553089/1729130169499635714/26cd9d6ec2e2494db1cd917e1385e5ed20231127.webp",
        "imgUrlList": null
      },
      {
        "id": "1729130724766765058",
        "goodsName": "Redmi G 游戏本 2022",
        "goodsPayType": 1,
        "goodsAmount": 300,
        "goodsPrice": 7499,
        "goodsDiscount": 4799,
        "goodsTypeCode": "1729001353678553089",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "新一代战力，K.O所有不服\n一块高刷电竞屏，是真正的杀手锏\n细入纤毫、疾速高刷，掌控全局战况\n不顾一切的全新设计和体验\n让每一次出场都更酷\nRedmi G 游戏本 2022\n点燃新战场",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": null,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1729001353678553089/1729130724766765058/a4005d4de83f402bbbe41f4e987ff59220231127.webp",
        "imgUrlList": null
      },
      {
        "id": "1729131875289518082",
        "goodsName": "Redmi Book 15E",
        "goodsPayType": 1,
        "goodsAmount": 200,
        "goodsPrice": 4999,
        "goodsDiscount": 2999,
        "goodsTypeCode": "1729001353678553089",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "超大处理器",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": null,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1729001353678553089/1729131875289518082/b6ca05a5781340a7ba06a9fce452f23620231127.webp",
        "imgUrlList": null
      },
      {
        "id": "1729132248163143682",
        "goodsName": "Redmi Book 14 + 小米平板5 Pro 12.4套装",
        "goodsPayType": 1,
        "goodsAmount": 200,
        "goodsPrice": 7498,
        "goodsDiscount": 7498,
        "goodsTypeCode": "1729001353678553089",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "Redmi Book 14 i5-12500H/16G/512G/2.8k/120Hz/金属-银色",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": null,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1729001353678553089/1729132248163143682/19a32ca473444d12a5dde44c0a35501e20231127.png",
        "imgUrlList": null
      },
      {
        "id": "1729132634802475010",
        "goodsName": "小米笔记本 Pro X 15",
        "goodsPayType": 1,
        "goodsAmount": 629,
        "goodsPrice": 6299,
        "goodsDiscount": 6299,
        "goodsTypeCode": "1729001353678553089",
        "status": 1,
        "goodsOrigin": null,
        "goodsAddress": "小米笔记本 Pro X 15",
        "goodsMarkCode": "1",
        "createTime": "2024-01-31 16:39:59",
        "sort": null,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1729001353678553089/1729132634802475010/fd248a3ff8fb49a982addbe61c0d47ed20231127.png",
        "imgUrlList": null
      }
    ]
  }
]//商品类型
            this.phoneList = [
  {
    "value": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636246843571916801/shu.webp",
    "key": "1358252184207151104"
  },
  {
    "value": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636246843571916801/shu2.webp",
    "key": "2"
  },
  {
    "value": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636246843571916801/shu3.webp",
    "key": "3"
  }
]
      
    }
  }
};
</script>
<style scoped>
@import "../assets/css/index.css";
</style>