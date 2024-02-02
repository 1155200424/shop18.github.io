<!--全部商品页面组件(包括全部商品,商品分类,商品搜索)-->
<template>
  <div class="goods" id="goods" name="goods">
    <!-- 面包屑 -->
    <div class="breadcrumb">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item to="/">首页</el-breadcrumb-item>
        <el-breadcrumb-item to="/goods">商品直营</el-breadcrumb-item>
        <el-breadcrumb-item v-if="search">搜索</el-breadcrumb-item>
        <el-breadcrumb-item v-else>{{ typeName }}</el-breadcrumb-item>
        <el-breadcrumb-item v-if="search">{{ search }}</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <!-- 面包屑END -->

    <!-- 分类标签 -->
    <div class="nav">
      <div class="product-nav">
        <div class="title">分类</div>
        <el-tabs v-model="activeName" type="card">
          <el-tab-pane v-for="item in categoryList" :key="item.id" :label="item.typeName" :name="'' + item.id" />
        </el-tabs>
      </div>
    </div>
    <!-- 分类标签END -->

    <!-- 主要内容区 -->
    <div class="main">
      <div class="list">
        <MyList :list="product" v-if="product.length > 0"></MyList>
        <div v-else class="none-product">抱歉没有找到相关的商品，请看看其他的商品</div>
      </div>
      <!-- 分页 -->
      <div class="pagination">
        <el-pagination background layout="prev, pager, next" :page-size="pageSize" :total="total"
          @current-change="currentChange"></el-pagination>
      </div>
      <!-- 分页END -->
    </div>
    <!-- 主要内容区END -->
  </div>
</template>
<script>
export default {
  data() {
    return {
      typeName: '全部',
      categoryList: [
        {
          "id": "0",
          "typeName": "全部",
        },
        {
          "id": "1729001353678553089",
          "typeName": "电脑",
          "imgType": "电子商品类",
          "status": 1,
          "sort": 600,
          "isHome": 1,
          "createTime": "2024-01-31 16:39:59"
        }
      ], //分类列表
      categoryID: '', // 分类id
      product: [], // 商品列表
      productList: [
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
        }
      ],
      
      total: 0, // 商品总量
      pageSize: 15, // 每页显示的商品数量
      currentPage: 1, //当前页码
      activeName: "-1", // 分类列表当前选中的id
      search: "" // 搜索条件
    };
  },
  created() {
    console.log('1111')
    // 获取分类列表
    this.getCategory();
  },
  activated() {
    this.activeName = "-1"; // 初始化分类列表当前选中的id为-1
    this.total = 0; // 初始化商品总量为0
    this.currentPage = 1; //初始化当前页码为1
    // 如果路由没有传递参数，默认为显示全部商品
    if (Object.keys(this.$route.query).length == 0) {
      this.categoryID = '0';
      this.activeName = "0";
      return;
    }
    // 如果路由传递了categoryID，则显示对应的分类商品
    if (this.$route.query.categoryID != undefined) {
      this.categoryID = this.$route.query.categoryID;
      if (this.$route.query.categoryID) {



        this.activeName = "" + this.$route.query.categoryID;


      }
      return;
      // debugger
    }
  },
  watch: {
    // 监听点击了哪个分类标签，通过修改分类id，响应相应的商品
    activeName: function (val) {
      if (!(this.product && this.product.length > 0)) {
        this.product = this.productList.filter(item => item.goodsTypeCode === this.$route.query.categoryID);
      }
      console.log(this.categoryList)
      if (val === 0) {
        this.typeName = '全部'
      } else {
        const result = this.categoryList.find(item => item.id === val);
        if (result) {
          this.typeName = result.typeName
          console.log(result);
        }

      }

      if (val == 0) {
        this.categoryID = '0';
      }
      if (val > 0) {
        this.categoryID = val;
      }
      // 初始化商品总量和当前页码
      this.total = 0;
      this.currentPage = 1;
        // 更新地址栏链接，方便刷新页面可以回到原来的页面
        this.$router.push({
          path: "/goods",
          query: { categoryID: this.categoryID }
        });
      

    },
    // 监听搜索条件，响应相应的商品
    search: function (val) {
      if (val != "") {
        this.getData()
      }
    },
    // 监听分类id，响应相应的商品
    categoryID: function () {
      this.getData();
      this.search = "";
    },
    // 监听路由变化，更新路由传递了搜索条件
    $route: function (val) {
      if (val.path == "/goods") {
        if (val.query.search != undefined) {
          this.activeName = "-1";
          this.currentPage = 1;
          this.total = 0;
          this.search = val.query.search;
        }
      }
    }
  },
  methods: {
    refreshPage() {
      this.$router.go(0); // 刷新当前路由
    },
    // 返回顶部
    backtop() {
      const timer = setInterval(function () {
        const top = document.documentElement.scrollTop || document.body.scrollTop;
        const speed = Math.floor(-top / 5);
        document.documentElement.scrollTop = document.body.scrollTop =
          top + speed;

        if (top === 0) {
          clearInterval(timer);
        }
      }, 20);
    },
    // 页码变化调用currentChange方法
    currentChange(currentPage) {
      this.currentPage = currentPage;
      if (this.search != "") {
        this.getData();
      } else {
        this.getData();
      }
      this.backtop();
    },
    // 向后端请求分类列表数据
    getCategory() {

    },
    // 向后端请求全部商品或分类商品数据
    getData() {
      if (this.categoryID.length != 0) {
        console.log(this.categoryID)
        if (this.categoryID === '0') {
          this.product = this.productList
          console.log("1234")
        } else {
      
          this.product = this.productList.filter(item => item.goodsTypeCode === this.categoryID);
          console.log(this.product)
          console.log(this.productList)
        }
      } else {
        this.product = this.productList
      }
      console.log(this.product)
    },
    // 通过搜索条件向后端请求商品数据
    getProductBySearch() {

    }
  }
}
  ;
</script>

<style scoped>
.goods {
  background-color: #f5f5f5;
}

/* 面包屑CSS */
.el-tabs--card .el-tabs__header {
  border-bottom: none;
}

.goods .breadcrumb {
  height: 50px;
  background-color: white;
}

.goods .breadcrumb .el-breadcrumb {
  width: 1225px;
  line-height: 30px;
  font-size: 16px;
  margin: 0 auto;
}

/* 面包屑CSS END */

/* 分类标签CSS */
.goods .nav {
  background-color: white;
}

.goods .nav .product-nav {
  width: 1225px;
  height: 40px;
  line-height: 40px;
  margin: 0 auto;
}

.nav .product-nav .title {
  width: 50px;
  font-size: 16px;
  font-weight: 700;
  float: left;
}

/* 分类标签CSS END */

/* 主要内容区CSS */
.goods .main {
  margin: 0 auto;
  max-width: 1225px;
}

.goods .main .list {
  min-height: 650px;
  padding-top: 14.5px;
  margin-left: -13.7px;
  overflow: auto;
}

.goods .main .pagination {
  height: 50px;
  text-align: center;
}

.goods .main .none-product {
  color: #333;
  margin-left: 13.7px;
}

/* 主要内容区CSS END */
</style>