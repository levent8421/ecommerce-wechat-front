<template>
  <div class="commodity-detail">
    <el-carousel height="200px">
      <el-carousel-item v-for="item in carousels" :key="item">
        <img :src="item" alt="" class="carousel-img">
      </el-carousel-item>
    </el-carousel>
    <div class="commodity">
      <h2>{{commodity.name}}</h2>
      <p>{{commodity.description}}</p>
      <p class="price">
        <span class="actual">{{commodity.price | toYuan}}</span>
        <span class="old">{{commodity.oldPrice | toYuan}}</span>
      </p>
      <p class="stock">
        <span>库存：{{commodity.stock}}</span>
        <span>已售：{{commodity.sold}}</span>
      </p>
    </div>
    <div class="shop">
      <p class="title-text">商家信息</p>
      <div class="shop-info">
        <div class="left">
          <h2>商家名称</h2>
          <p>常州市武进区xxxx</p>
          <p>13235123512</p>
        </div>
        <div class="right">
          <i class="el-icon-phone"></i>
        </div>
      </div>
    </div>
    <div class="detail-html-wrapper">
      <p class="title-text">详细信息</p>
      <div class="detail-html">
        详细信息文本
      </div>
    </div>
    <div class="bottom-buttons">
      <button class="btn-shop">
        <i class="el-icon-s-shop"></i>
        <span>店铺</span>
      </button>
      <button class="btn-service">
        <i class="el-icon-service"></i>
        <span>客服</span>
      </button>
      <button class="btn-buy" @click="handleBuy">立即购买</button>
    </div>
    <commodity-share-dialog :returnMoney="commodity.returnMoney" :show="showShare" :code="shareCode"
                            @share="handleShare"/>
  </div>
</template>

<script>
import CommodityShareDialog from './CommodityShareDialog'

export default {
  created () {
    this.id = this.$route.params.id
  },
  components: {
    CommodityShareDialog
  },
  data () {
    return {
      carousels: [
        'http://img.lanrentuku.com/img/allimg/1707/14988864745279.jpg',
        'http://img.lanrentuku.com/img/allimg/1709/1506069090817.jpg',
        'http://py.66wz.com/pic/003/005/918/00300591864_99c2d0c6.jpg',
        'http://py.66wz.com/pic/003/005/910/00300591038_61dbd7a8.jpg'
      ],
      commodity: {
        name: '火龙果',
        description: '资讯类信息文案可以打满多行资讯类信息文案可以打满多行资讯类信息文案可以打满多行。',
        price: '100.00',
        oldPrice: '125.00',
        stock: 100,
        sold: 109,
        returnMoney: 7
      },
      showShare: true,
      shareCode: '10010'
    }
  },
  name: 'CommodityDetail',
  methods: {
    handleShare (code) {
      alert('share' + code)
    },
    handleBuy () {
      const id = this.$route.params.id
      this.$router.push({name: 'Buy', params: {id}})
      this.$store.dispatch('setTitle', '购买')
    }
  }
}
</script>

<style scoped lang="less">
  .commodity-detail {
    .title-text {
      font-size: .9rem;
      margin: 10px 0 0 10px;
      padding: 0;
      color: #AEAEAE;
    }

    .carousel-img {
      width: 100%;
      height: 100%;
    }

    .commodity {
      padding: 0 10px 5px 10px;
      background-color: white;

      h2 {
        color: #666666;
        margin: 5px 0;
        padding: 0;
        font-size: 1.2rem;
        font-weight: normal;
      }

      p {
        color: #666666;
        margin: 20px 0;
        font-size: .8rem;
      }

      .price {
        .actual {
          color: red;
          font-size: 1.5rem;
        }

        .old {
          font-size: .9rem;
          color: #666666;
          margin-left: 10px;
          text-decoration: line-through;
        }
      }

      .stock {
        display: flex;
        justify-content: space-between;
      }
    }

    .shop {
      .shop-info {
        display: flex;
        justify-content: space-between;
        background-color: white;
        padding: 0 10px;

        .left {
          h2 {
            color: #666666;
            font-size: 1.2rem;
            font-weight: normal;
            margin: 0;
            padding: 0;
          }

          p {
            margin: 0;
            padding: 0;
            font-size: .9rem;
            color: #AEAEAE;
          }
        }

        .right {
          i {
            line-height: 60px;
            font-size: 2.1rem;
            color: #FF9900;
          }
        }
      }
    }

    .detail-html-wrapper {
      margin-bottom: 50px;

      .detail-html {
        background-color: white;
        height: 500px;
      }
    }

    .bottom-buttons {
      position: fixed;
      height: 50px;
      width: 100%;
      bottom: 50px;
      left: 0;
      border-top: 1px solid #DDDDDD;
      background-color: white;
      display: flex;
      justify-content: space-between;

      button {
        background-color: transparent;
        border: none;
        outline: none;

        &:first-child {
          margin-left: 30px;
        }
      }

      .btn-buy {
        width: 50%;
        border-radius: 3px;
        background-color: red;
        color: white;
        font-size: 1.1rem;
        line-height: 50px;
      }

      .btn-shop, .btn-service {
        text-align: center;

        i {
          display: block;
          font-size: 1.8rem;
        }

        span {
          display: block;
        }
      }

      .btn-shop {
        color: #FF9900;
      }

      .btn-service {
        color: #666666;
      }
    }
  }
</style>
