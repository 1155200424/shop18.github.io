<!--商品详情页面组件 -->
<template>
  <div id="details">
    <div class="breadcrumb">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item to="/">首页</el-breadcrumb-item>
        <el-breadcrumb-item to="/goods">商品直营</el-breadcrumb-item>
        <el-breadcrumb-item :to="{ path: '/goods', query: {categoryID:typeId} }">{{typeName}}</el-breadcrumb-item>
        <el-breadcrumb-item></el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <!-- 头部 -->
    <div class="page-header">
      <div class="title">
        <p>{{ productDetails.goodsName }}</p>
      </div>
    </div>
    <!-- 头部END -->

    <!-- 主要内容 -->
    <div class="main">
      <div class="block">
        <div v-if="productPicture">
          <img
            style="height:560px; width: 560px"
            :src="require(`../assets${productPicture}`)" 
          
          />
        </div>
      </div>
      <!-- 左侧商品轮播图END -->

      <!-- 右侧内容区 -->
      <div class="content">
        <h1 class="name">{{ productDetails.goodsName }}</h1>
        <p class="intro">{{ productDetails.goodsAddress }}</p>
        <div
          style="display:flex;justify-content:space-between;align-items: center;"
        >
          <span class="store">{{ productDetails.goodsOrigin }}</span>
          <div style="fontWeight:bold;" v-show="seckill">
            <span class="store">限时秒杀：</span>
            <span class="time">{{hour}}</span> : 
            <span class="time">{{min}}</span> : 
            <span class="time">{{sec}}</span>
          </div>
        </div>
        <div class="price">
          <span>{{ productDetails.goodsDiscount }}元</span>
          <span
            v-show="productDetails.goodsDiscount != productDetails.goodsPrice"
            class="del"
            >{{ productDetails.goodsPrice }}元</span
          >
        </div>
        <div class="pro-list">
          <span class="pro-name">{{ productDetails.goodsName }}</span>
          <span class="pro-price">
            <span>{{ productDetails.goodsDiscount }}元</span>
            <span
              v-show="productDetails.goodsDiscount != productDetails.goodsPrice"
              class="pro-del"
              >{{ productDetails.goodsPrice }}元</span
            >
          </span>
          <p class="price-sum">
            {{ seckill ? "秒杀价" : "总计" }} :
            {{ productDetails.goodsDiscount }}元
          </p>
        </div>
        <!-- 内容区底部按钮 -->
        <div class="button">
          <el-button
            class="shop-cart"
            :disabled="dis"
            v-if="seckill"
            >{{seckillText}}</el-button
          >
          <el-button
            class="shop-cart"
            :disabled="dis"
            v-else
            >加入购物车</el-button
          >
        </div>
        <!-- 内容区底部按钮END -->
      </div>
      <!-- 右侧内容区END -->
    </div>
    <div class="sun_pl">
      <p class="sun_p_lj">商品参数</p>
      <p>{{ productDetails.goodsAddress}}</p>
    </div>

  </div>
</template>
<script>

export default {
  data() {
    return {
      typeName:'电脑',
      typeId:'1729001353678553089',
      dis: false, // 控制“加入购物车按钮是否可用”
      productID: "", // 商品id
      productDetails: "", // 商品详细信息
      productPicture: "", // 商品图片
      productTag: "", // 标签
      arr: [],
      seckill: this.$route.query.seckill == "true",
      hour: "00",
      min: "00",
      sec: "00",
      goodsList: [
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
        "id": "1636246843571916801",
        "goodsName": "华为智选 Hi nova 9z",
        "goodsPayType": 1,
        "goodsAmount": 998,
        "goodsPrice": 1000,
        "goodsDiscount": 200,
        "goodsTypeCode": "1636246470664736770",
        "status": 1,
        "goodsOrigin": "湖北",
        "goodsAddress": "华为智选 Hi nova 9z 5G全网通手机 6.67英寸120Hz原彩屏hinova 6400万像素超清",
        "goodsMarkCode": "1,5,6",
        "createTime": "2024-01-31 16:39:59",
        "sort": 200,
        "goodeUserType": 0,
        "imgUrl": "/schoolMall/MALL_GOODS_IMG/1636246470664736770/1636246843571916801/9a456ca687c749e2ac4a0270aa9f083420230515.dpg",
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
      },
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
    ],

    };
  },
  // 通过路由获取商品id
  activated() {
    console.log('进入页面2');
    console.log(this.$route.query.seckill);
    if (this.$route.query.productID != undefined) {
      this.productID = this.$route.query.productID;
    }

      
  
  },
  watch: {
    // 监听商品id的变化，请求后端获取商品数据
    productID: function(val) {
      this.getDetails(val);
      this.getDetailsPicture(val);
    },
  },
  methods: {
    // 获取商品详细信息
    getDetails(val) {
         console.log(this.goodsList)
          this.productDetails = this.goodsList.find(item => item.id === val);
          // this.productDetails = res.data.data.information;
          this.productPicture = this.productDetails.imgUrl;
    },
    // 获取商品图片
    getDetailsPicture(val) {
      console.log(val);
    },

  }
};
</script>
<style lang="less">
.time{
  background-color: #ff6700;
  color: white;
  padding: 3px;
  border-radius: 3px;
}
/* 头部CSS */
#details .page-header {
  height: 64px;
  margin-top: -20px;
  z-index: 4;
  background: #fff;
  border-bottom: 1px solid #e0e0e0;
  -webkit-box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.07);
  box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.07);
}
#details .breadcrumb {
  height: 50px;
  background-color: white;
}

#details .breadcrumb .el-breadcrumb {
  width: 1225px;
  line-height: 30px;
  font-size: 16px;
  margin: 0 auto;
}
#details .page-header .title {
  width: 1225px;
  height: 64px;
  line-height: 64px;
  font-size: 18px;
  font-weight: 400;
  color: #212121;
  margin: 0 auto;
}

#details .page-header .title p {
  float: left;
}

#details .page-header .title .list {
  height: 64px;
  float: right;
}

#details .page-header .title .list li {
  float: left;
  margin-left: 20px;
}

#details .page-header .title .list li a {
  font-size: 14px;
  color: #616161;
}

#details .page-header .title .list li a:hover {
  font-size: 14px;
  color: #ff6700;
}

/* 头部CSS END */

/* 主要内容CSS */
#details .main {
  width: 1225px;
  height: 560px;
  padding-top: 30px;
  margin: 0 auto;
}

#details .main .block {
  float: left;
  width: 560px;
  height: 560px;
}

#details .el-carousel .el-carousel__indicator .el-carousel__button {
  background-color: rgba(163, 163, 163, 0.8);
}

#details .main .content {
  float: left;
  margin-left: 25px;
  width: 640px;
}

#details .main .content .name {
  height: 30px;
  line-height: 30px;
  font-size: 24px;
  font-weight: normal;
  color: #212121;
}

#details .main .content .intro {
  color: #b0b0b0;
  padding-top: 10px;
}

#details .main .content .store {
  color: #ff6700;
  padding-top: 10px;
}

#details .main .content .price {
  display: block;
  font-size: 18px;
  color: #ff6700;
  border-bottom: 1px solid #e0e0e0;
  padding: 25px 0 25px;
}

#details .main .content .price .del {
  font-size: 14px;
  margin-left: 10px;
  color: #b0b0b0;
  text-decoration: line-through;
}

#details .main .content .pro-list {
  background: #f9f9fa;
  padding: 30px 60px;
  margin: 50px 0 50px;
}

#details .main .content .pro-list span {
  line-height: 30px;
  color: #616161;
}

#details .main .content .pro-list .pro-price {
  float: right;
}

#details .main .content .pro-list .pro-price .pro-del {
  margin-left: 10px;
  text-decoration: line-through;
}

#details .main .content .pro-list .price-sum {
  color: #ff6700;
  font-size: 24px;
  padding-top: 20px;
}

#details .main .content .button {
  height: 55px;
  margin: 10px 0 20px 0;
}

#details .main .content .button .el-button {
  float: left;
  height: 55px;
  font-size: 16px;
  color: #fff;
  border: none;
  text-align: center;
}

#details .main .content .button .shop-cart {
  width: 340px;
  background-color: #ff6700;
}

#details .main .content .button .shop-cart:hover {
  background-color: #f25807;
}

#details .main .content .button .like {
  width: 260px;
  margin-left: 40px;
  background-color: #b0b0b0;
}

#details .main .content .button .like:hover {
  background-color: #757575;
}

#details .main .content .pro-policy li {
  float: left;
  margin-right: 20px;
  color: #b0b0b0;
}

.sun_pl {
  width: 65%;
  margin: auto;

  .sun_p_lj {
    font-size: 25px;
    text-align: center;
    border-bottom: 1px solid #e0e0e0;
    border-top: 1px solid #e0e0e0;
    padding: 20px;
    margin: 20px;
  }
}

/* 主要内容CSS END */
</style>