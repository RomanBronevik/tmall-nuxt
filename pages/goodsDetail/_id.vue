<!--
 * @Author: your name
 * @Date: 2020-01-21 08:56:41
 * @LastEditTime: 2020-02-24 22:28:02
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \nuxt\pages\goodsDetail.vue
 -->

<template>
  <div style="min-height:3000px">
    <site-nav :width="990"></site-nav>
    <nav class="navigation-con">
      <ul class="navigation-bar">
        <li>
          <a>{{shop&&shop.shop_name?shop.shop_name:"官网旗舰店"}}</a>
        </li>
        <li>
          <a>首页</a>
        </li>
        <li>
          <a>新品到店</a>
        </li>
        <li>
          <a>男士特区</a>
        </li>
        <li>
          <a>女士特区</a>
        </li>
        <li>
          <a>处理中心</a>
        </li>
        <li>
          <a>会员臻选</a>
        </li>
        <li>
          <a>全部商品</a>
        </li>
        <li>
          <label style="position: relative;">
            <img
              src="//gdp.alicdn.com/imgextra/i1/1917047079/O1CN01U91D4t22AEE0H16cJ_!!1917047079.png"
              class="navsearch-btn"
            />
            <input type="text" class="navigation-input" />
          </label>
        </li>
      </ul>
    </nav>

    <article id="detail">
      <div class="tm-detail-meta">
        <section class="tb-gallery">
          <div class="tb-booth">
            <img
              v-if="previewParams.prevImg"
              id="J_ImgBooth"
              :src="previewParams.prevImg+'_430x430q90.jpg'"
            />
          </div>
          <div class="tb-thumb-warp">
            <ul id="J_UlThumb" class="tb-thumb tm-clear">
              <!-- class="tb-selected" -->
              <li
                v-for="(item,index) of preview "
                :key="item.id"
                :class="{'tb-selected':previewParams.previewIndex===index}"
                @mouseenter="changePrevview(index,item.img_url)"
              >
                <a>
                  <img :src="item.img_url&&item.img_url+'_60x60q90.jpg'" alt="商品预览图" />
                </a>
              </li>
            </ul>
          </div>
          <div class="tm-action">
            <a id="J_AddFavorite">
              <i class="iconfont iconshoucangxuanzhong"></i>
              <span>收藏商品</span>
              <span id="J_CollectCount">（159880人气）</span>
            </a>
            <span id="J_EditItem">
              <a>举报</a>
            </span>
          </div>
        </section>
        <section class="tb-property">
          <div class="tb-detail-hd">
            <h1>
              <a href>{{goods_name}}</a>
            </h1>
          </div>
          <div class="tm-fcs-panel">
            <dl class="tm-price-panel tm-price-cur" id="J_StrPriceModBox">
              <dt class="tb-metatit">价格</dt>
              <dd>
                <em class="tm-yen">¥</em>
                <span class="tm-price">{{price}}</span>
              </dd>
            </dl>
          </div>
          <div class="tb-meta">
            <dl class="tm-delivery-panel" id="J_RSPostageCont">
              <dt class="tb-metatit">运费</dt>
              <dd>
                <div class="tb-postAge">
                  <span class="tb-deliveryAdd" id="J_deliveryAdd">上海</span>至
                  <span id="J_AddrSelectTrigger" class="mui_addr_tri" combo-level="3">
                    <span
                      role="button"
                      tabindex="0"
                      aria-haspopup="true"
                      data-code="440300"
                      class="mui_addr_tri_1"
                    >
                      深圳
                      <i class="iconfont icondiquxialajiantou"></i>
                    </span>
                    <span
                      role="button"
                      tabindex="0"
                      aria-haspopup="true"
                      data-code="440303"
                      class="mui_addr_tri_2"
                    >
                      罗湖区
                      <i class="iconfont icondiquxialajiantou"></i>
                    </span>
                  </span>
                  <div id="J_PostageToggleCont" class="tb-postAge-info">
                    <p>
                      <span>快递: 0.00</span>
                    </p>
                  </div>
                </div>
                <div class="signText">付款后3天内发货</div>
              </dd>
            </dl>
          </div>
          <ul class="tm-ind-panel">
            <li class="tm-ind-item tm-ind-reviewCount canClick tm-line3" id="J_ItemRates">
              <div class="tm-indcon">
                <span class="tm-label">累计评价</span>
                <span class="tm-count">24536</span>
              </div>
            </li>
            <li class="tm-ind-item tm-ind-emPointCount" data-spm="1000988">
              <div class="tm-indcon">
                <a href="//vip.tmall.com/vip/index.htm" target="_blank">
                  <span class="tm-label">送天猫积分</span>
                  <span class="tm-count">{{Math.ceil(price/10)}}</span>
                </a>
              </div>
            </li>
          </ul>
          <div class="tb-key">
            <div class="tb-skin" :class="{'tb-no-choose':chooseSpecWarn}">
              <p class="tb-note-title">
                请选择您要的商品信息
                <b class="J_PanelCloser" @click="resetSpecWar">x</b>
              </p>
              <div class="tb-sku">
                <dl class="tb-prop" v-for="spec in spec" :key="spec.id">
                  <dt class="tb-metatit">{{spec.spec_name}}</dt>
                  <dd>
                    <ul class="tm-relate-list" :class="{'tb-img':spec.values[0].spec_value_cover}">
                      <li
                        v-for="specValue in spec.values"
                        :key="specValue.id"
                        :class="{'tb-selected':params.spec[spec.id]===specValue.id}"
                      >
                        <a
                          v-if="specValue.spec_value_cover"
                          :style="{background:`url(${specValue.spec_value_cover+'_40x40q90.jpg'}`}"
                          @click="chooseSpec(spec.id,specValue.id,specValue.spec_value_cover)"
                        >{{specValue.spec_value}}</a>
                        <a v-else @click="chooseSpec(spec.id,specValue.id)">{{specValue.spec_value}}</a>
                        <i>已选中</i>
                      </li>
                    </ul>
                  </dd>
                </dl>

                <dl class="tb-amount tm-clear">
                  <dt class="tb-metatit">数量</dt>
                  <dd id="J_Amount" style="display: flex;align-items: center;">
                    <el-input-number
                      style="width: 67px;"
                      v-model="params.num"
                      controls-position="right"
                      :min="1"
                    ></el-input-number>
                    <p class="tb-hidden" v-if="skuData.stock">{{`库存${skuData.stock}件`}}</p>
                  </dd>
                </dl>
                <div class="tb-action tm-clear">
                  <div class="tb-btn-buy tb-btn-sku" v-show="buyNow.show">
                    <a
                      id="J_LinkBuy"
                      href="#"
                      rel="nofollow"
                      data-addfastbuy="true"
                      title="点击此按钮，到下一步确认购买信息。"
                      role="button"
                      @click="buyNowSumbit"
                      v-show="buyNow.show"
                    >{{buyNow.text}}</a>
                  </div>
                  <div class="tb-btn-basket tb-btn-sku" v-show="shopCart.show">
                    <a
                      href="#"
                      rel="nofollow"
                      id="J_LinkBasket"
                      role="button"
                      v-show="shopCart.show"
                      @click="addToShoppingCart"
                    >
                      <i class="iconfont icongouwuche2"></i>
                      {{shopCart.text}}
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>
      </div>
      <el-dialog :visible.sync="showLoginBox" width="25%" center>
        <login-view @loginSucceed="loginSucceed"></login-view>
      </el-dialog>
    </article>

    <article id="bd">
      <section style="width:190px;">
        <div class="side-shop-info" id="side-shop-info">
          <h3 class="hd">
            <div class="name">
              <a href class="shopLink">{{shop&&shop.shop_name?shop.shop_name:"官网旗舰店"}}</a>
              <span class="ww-light ww-small">
                <a class="ww-inline ww-online" title="点此可以直接和卖家交流选好的宝贝，或相互交流网购体验，还支持语音视频噢。"></a>
              </span>
            </div>
          </h3>
          <div class="main-info">
            <div class="shopdsr-item">
              <div class="shopdsr-title">描 述</div>
              <div class="shopdsr-score shopdsr-score-equal-ctrl">
                <span class="shopdsr-score-con">4.8</span>
                <i class="iconfont shopdsr-iconfont iconjian"></i>
              </div>
            </div>
            <div class="shopdsr-item">
              <div class="shopdsr-title">描 述</div>
              <div class="shopdsr-score shopdsr-score-equal-ctrl">
                <span class="shopdsr-score-con">4.8</span>
                <i class="iconfont shopdsr-iconfont iconjian"></i>
              </div>
            </div>
            <div class="shopdsr-item">
              <div class="shopdsr-title">描 述</div>
              <div class="shopdsr-score shopdsr-score-equal-ctrl">
                <span class="shopdsr-score-con">4.8</span>
                <i class="iconfont shopdsr-iconfont iconjian"></i>
              </div>
            </div>
          </div>
          <div class="btnArea">
            <a class="enterShop">进店逛逛</a>
            <a
              id="xshop_collection_href"
              class="J_PopupTrigger collection xshop_sc J_TDialogTrigger J_TokenSign favShop"
            >收藏店铺</a>
          </div>
        </div>
      </section>
      <section style="width:790px">
        <el-tabs type="border-card">
          <el-tab-pane label="商品详情">
            <div id="attributes" class="attributes">
              <div class="attributes-list" id="J_AttrList">
                <div
                  class="tm-clear tb-hidden tm_brandAttr"
                  id="J_BrandAttr"
                  style="display: block;"
                >
                  <div class="name">
                    品牌名称：
                    <b class="J_EbrandLogo" target="_blank">{{brand?brand.brand_name:"无"}}</b>
                  </div>
                </div>
              </div>
            </div>
            <div id="description" class="J_DetailSection tshop-psm tshop-psm-bdetaildes tm-curTab">
              <h4 class="hd">商品详情</h4>
              <div class="content ke-post">
                <el-image v-for="item in content" :key="item.id" :src="item.image" lazy></el-image>
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="累计评价">累计评价</el-tab-pane>
        </el-tabs>
      </section>
    </article>
  </div>
</template>

<script>
import loginView from '@/components/common/login-view'
import { goodsDetails } from '~/assets/api/goods-detail'
import * as JwtService from '@/assets/common/JwtService.js'
import siteNav from '~/components/common/site-nav.vue'
export default {
  components: {
    'login-view': loginView,
    'site-nav': siteNav
  },
  layout: 'noNav',
  data() {
    return {
      previewParams: {
        previewIndex: 0,
        prevImg: false
      },
      chooseSpecWarn: false,
      showLoginBox: false,
      params: {
        num: 1,
        spec: {}
      },
      buyNow: {
        show: true,
        text: '立即购买'
      },
      shopCart: {
        show: true,
        text: '加入购物车'
      },
      skuData: false,
      activeBtn: false
    }
  },
  methods: {
    loginSucceed() {
      this.showLoginBox = false
      if (this.activeBtn === 'shopCart') {
        this.addToShoppingCart()
      } else if (this.activeBtn === 'buyNow') {
        this.buyNowSumbit()
      }
    },
    /**
     * @description: spec 是否未false
     * @param {type}
     * @return:
     */
    validateSpecIsEmpty() {
      let spec = this.params.spec
      for (let value of Object.values(spec)) {
        if (!value) {
          return true
        }
      }
      return false
    },
    validateIsLogin() {
      if (this.$store.getters['isAuthenticated']) {
        return true
      } else {
        this.showLoginBox = true
      }
    },
    validateSubmit(activeBtn) {
      this.activeBtn = activeBtn
      if (this.validateSpecIsEmpty()) {
        this.chooseSpecWarn = true
        let handlerBtn = { show: false, text: '确认' }
        Object.assign(this.buyNow, handlerBtn)
        Object.assign(this.shopCart, handlerBtn)
        return false
      }
      if (!this.validateIsLogin()) {
        return false
      }
      this.resetSpecWar()
      return true
    },
    resetSpecWar() {
      this.chooseSpecWarn = false
      Object.assign(this.buyNow, { show: true, text: '立即购买' })
      Object.assign(this.shopCart, { show: true, text: '加入购物车' })
    },
    addToShoppingCart() {
      if (this.validateSubmit('shopCart')) {
        if (!this.skuData) {
          this.$message({
            showClose: true,
            message: '购物车错误,请稍后再试',
            type: 'warning'
          })
        }
        let params = {
          spuId: this.$route.params.id,
          skuId: this.skuData.id,
          memberId: String(this.$store.getters['currentUser'].id),
          product_amount: this.params.num
        }
        this.$store
          .dispatch('goods/addShopCart', params)
          .then(item => {
            const h = this.$createElement
            this.$message({
              showClose: false,
              message: h('p', { style: 'font-size:16px' }, [
                h('span', null, '加入'),
                h(
                  'a',
                  {
                    style:
                      'color: #ff0036;text-decoration: underline;padding: 5px;',
                    domProps: {
                      href: '/shopCart'
                    }
                  },
                  '购物车'
                ),
                h('span', null, '成功')
              ]),
              type: 'success',
              duration: 0
            })
          })
          .catch(error => {
            this.$message({
              showClose: true,
              message: '加入购物车失败,请稍后再试',
              type: 'error'
            })
          })
      }
    },
    handleShoppingCart() {},
    /**
     * @description: 立即购买
     * @param {type}
     * @return:
     */
    buyNowSumbit() {
      if (this.validateSubmit('buyNow')) {
        let params = {
          skuId: this.skuData.id,
          product_amount: this.params.num
        }
        this.$store.commit('confirmOrder/CREATE_PARAMS', [params])
        this.$router.push('/confirmOrder')
      }
    },
    /**
     * @description: 修改预览图下表
     * @param {
     *  index: 下标
     *  img  : 预览图img
     * }
     */

    changePrevview(index, img) {
      this.previewParams.previewIndex = index
      this.previewParams.prevImg = img
    },
    /**
     * @description: 修改选中的spec
     * @param {
     *  key   : params.spec的属性名
     *  value : params.spec的属性值
     *  src   : 预览大图的src
     * }
     * @return:
     */

    chooseSpec(key, value, src) {
      let spec = this.params.spec
      if (!spec[key]) {
        this.$set(spec, key, value)
      } else {
        spec[key] = value
      }
      if (src) {
        this.changePrevview(-1, src)
      }
    }
  },
  async asyncData({ params: { id }, error, $axios }) {
    if (id) {
      let data = await $axios.$get('/goods/goodsDetails', {
        params: { spu_id: id }
      })
      let spec = {}
      data.spec.forEach(({ id }) => {
        spec[id] = false
      })
      data.params = { num: 1, spec }
      return data
    } else {
      error({ statusCode: 400, message: '没有spu_id参数' })
    }
  },
  mounted() {
    this.preview[0]
      ? (this.previewParams.prevImg = this.preview[0].img_url)
      : ''
  },
  watch: {
    'params.spec': {
      async handler(to) {
        if (!this.validateSpecIsEmpty()) {
          if (this.chooseSpecWarn) {
            this[this.activeBtn].show = true
          }
          let params = { spuId: this.$route.params.id }
          let tempList = []
          for (let value of Object.values(this.params.spec)) {
            tempList.push(value)
          }
          params.specData = tempList
          let skuData = await this.$store.dispatch('goods/findSku', params)
          this.skuData = skuData[0]
        }
      },
      deep: true
    }
  }
}
</script>

<style scoped lang="scss">
.tb-hidden{
    color: #878787;
    margin-left: 1.2em;
}
/deep/body{
  min-height: 3000px;
}
.mui-dialog-header {
    background-image: url(//img.alicdn.com/tfs/TB1VLoORXXXXXc4XXXXXXXXXXXX-132-41.png)!important;
    background-color: #ff0036!important;
    border-bottom: none!important;
}
.mui-dialog-header {
    height: 35px;
    line-height: 35px;
    padding-left: 10px;
    border-bottom: 1px solid #8c0400;
    background-color: #B6000C;
    background-position: 20px 10px;
    font-size: 14px;
    font-weight: 700;
}
.mui-dialog-header,.mui-dialog-close {
    background: url(//img.alicdn.com/tps/i2/T1CdBMFkNeXXb23GA.-132-41.png) no-repeat;
}
.tb-no-choose .tb-note-title{
  display: block
}
.tb-no-choose .tb-btn-sku a {
    display: block;
    height: 34px !important;
    line-height: 34px !important;
    width: 76px !important;
    background-color: #ff0036 !important;
    border: 1px solid #ff0036 !important;
    color: #fff !important;
}
.tb-note-title b {
    position: absolute;
    z-index: 10;
    margin: 0 10px 8px 0;
    height: 8px;
    width: 8px;
    right: 0;
    top: 0;
    cursor: pointer;
    color: #b40000;
    font-size: 14px;
    font-weight: bolder;
    font-family: arial;
}
.tb-note-title {
    display: none;
    background-color: #fff8f7;
    border-bottom: 1px solid #f3e9e7;
    height: 24px;
    position: relative;
    line-height: 24px;
    margin: -8px -8px 5px;
    padding-left: 8px;
    z-index: 10;
}
.tb-no-choose{
      border: 2px solid #c00;
    position: relative;
    z-index: 10;
    background-color: #fff;
    padding: 8px 8px 14px !important;
    margin: -21px 0 0 -10px;
}
#J_Attrs, #J_Attrs h4.hd, #description h4.hd, .TMDtemai #J_Reviews, .tm-tabOther #J_DcBottomRightWrap, .tm-tabOther #J_DcTopRightWrap, .tm-tabOther #J_Detail h4.hd, .tm-tabOther #J_LadeMap, .tm-tabOther #J_store, .tm-tabOther #attributes, .tm-tabOther #auto-delivery, .tm-tabOther #autofill, .tm-tabOther #detail div.msg, .tm-tabOther #extra-attributes, .tm-tabOther #item-flash, .tm-tabOther #mall-banner, .tm-tabOther #trydetail, .tm-tabOther .J_DetailSection, .w1190 .tm-tabOther .tm-descCate, .w990 .tm-tabOther .tm-bd-side {
    display: none;
}
#description {
    width: auto;
    padding: 0;
}
#description .content {
    width: 100%;
    margin: 10px 0 0;
    overflow: hidden;
}
/deep/.el-tabs--border-card{
       border: none; 
    box-shadow: none; 
}
/deep/.el-tabs--border-card>.el-tabs__content {
    padding: 0;
}
/deep/.el-tabs--border-card>.el-tabs__header{
      border: 1px solid #DCDFE6;
    box-shadow: 0 1px 4px 0 rgba(0,0,0,.12), 0 0 6px 0 rgba(0,0,0,.04);
}
#J_BrandAttr .name b {
    color: #333;
    font-weight: 400;
}
#J_BrandAttr .name {
    color: #666;
    float: left;
    margin-right: 15px;
}
#J_BrandAttr {
    padding: 8px 20px 10px;
    border-top: 1px solid #e6e6e6;
    height: 40px;
    line-height: 40px;
}
#attributes div.attributes-list {
    clear: both;
    border: 1px solid #e6e6e6;
    border-top: none;
    margin-bottom: 10px;
}
#side-shop-info {
    border: 1px solid #e5e5e5;
    padding: 0 0 15px;
    margin-bottom: 10px;
}
#side-shop-info .btnArea .favShop {
    float: right;
    text-decoration: none;
    background-color: #f5f5f5;
    border: 1px solid #ccc;
    color: #333;
}
#side-shop-info .btnArea .enterShop, #side-shop-info .btnArea .favShop {
    float: left;
    width: 70px;
    height: 24px;
    line-height: 24px;
    text-align: center;
}
#side-shop-info .btnArea {
    overflow: hidden;
    margin: 15px auto 0;
    width: 150px;
}
#side-shop-info .btnArea .enterShop, #side-shop-info .btnArea .enterShop:hover {
    text-decoration: none;
    border: 1px solid #333;
    background-color: #333;
    color: #fff;
}
.shopdsr-iconfont{
     margin-top: 2px;
    margin-left: 2px;
    font-size: 10px !important;
}
#side-shop-info .main-info {
    overflow: hidden;
    width: 130px;
    margin: 0 auto;
    cursor: pointer;
    position: relative;
}
#side-shop-info .main-info .shopdsr-score-equal {
    color: #ff0036;
    background: 0 0;
    text-decoration: none;
    height: 9px;
    width: 8px;
    right: 2px;
    top: 5px;
    position: absolute;
}
#side-shop-info .main-info .shopdsr-item {
    float: left;
    color: #999;
    width: 36px;
    height: 36px;
    margin: 15px 7px 0 0;
    position: relative;
}
#side-shop-info .main-info .shopdsr-score {
    color: #ff0036;
    padding-left: 5px;
        display: flex;
    height: 18px;
    width: 31px;
    position: relative;
    overflow: hidden;
}
#side-shop-info .main-info .shopdsr-title {
    text-align: center;
    font-family: "\5b8b\4f53";
}
#side-shop-info .main-info .shopdsr-score {
    color: #ff0036;
    padding-left: 5px;
    height: 18px;
    width: 31px;
    position: relative;
    overflow: hidden;
}
.ww-light {
    overflow: hidden;
}
.ww-small .ww-online {
    background-position: -80px 0;
}
.ww-light a {
    background-image: url(//img.alicdn.com/tps/i1/T15AD7FFFaXXbJnvQ_-130-60.gif);
    background-image: -webkit-image-set(url(//img.alicdn.com/tps/i1/T15AD7FFFaXXbJnvQ_-130-60.gif) 1x,url(//img.alicdn.com/tps/i4/T1Rsz7FPJaXXbZhKn7-520-240.gif) 4x);
    background-image: -moz-image-set(url(//img.alicdn.com/tps/i1/T15AD7FFFaXXbJnvQ_-130-60.gif) 1x,url(//img.alicdn.com/tps/i4/T1Rsz7FPJaXXbZhKn7-520-240.gif) 4x);
    background-image: -o-image-set(url(//img.alicdn.com/tps/i1/T15AD7FFFaXXbJnvQ_-130-60.gif) 1x,url(//img.alicdn.com/tps/i4/T1Rsz7FPJaXXbZhKn7-520-240.gif) 4x);
    background-image: -ms-image-set(url(//img.alicdn.com/tps/i1/T15AD7FFFaXXbJnvQ_-130-60.gif) 1x,url(//img.alicdn.com/tps/i4/T1Rsz7FPJaXXbZhKn7-520-240.gif) 4x);
    text-decoration: none!important;
    width: 20px;
    height: 20px;
    zoom: 1;
}
.ww-inline {
    display: inline-block;
    vertical-align: text-bottom;
}
#side-shop-info .hd .shopLink {
  color: #333;
  font-size: 12px;
}
.side-shop-info .shop-intro {
  background-color: #fff;
}
.side-shop-info .hd .shopLink {
  color: #333;
  font-size: 12px;
}
.side-shop-info .hd {
  padding: 0 0 0 15px;
  height: 48px;
  line-height: 48px;
  background-color: #fafafa;
  border-bottom: 1px solid #e5e5e5;
}
#bd {
  width: 990px !important;
  margin: auto;
  display: flex;
  justify-content: space-between;
}
/deep/.el-tabs--border-card > .el-tabs__header .el-tabs__item.is-active {
  color: red;
  font-weight: bold;
  position: relative;
  border-top: 3px solid #ff0036;
  box-sizing: border-box;
  &::after {
    content: " ";
    display: block;
    border-width: 5px;
    border-style: solid;
    border-color: #ff0036 transparent transparent;
    width: 0;
    height: 0;
    font-family: arial;
    position: absolute;
    top: -1px;
    left: 50%;
    margin-left: -5px;
  }
}
.tb-prop .tb-img li a {
  text-decoration: none;
  width: auto !important;
  background-position: left center !important;
  background-repeat: no-repeat !important;
  padding: 0 9px 0 45px;
}
.tb-prop .tb-img li a {
  text-decoration: none;
  width: auto !important;
  background-position: left center !important;
  padding: 0 9px 0 45px !important;
  width: 38px !important;
  height: 38px;
  padding: 0;
  line-height: 38px;
  background-repeat: no-repeat;
  outline: 0;
  background-position: center center;
}
.tb-key .tb-selected i {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAwAAAAMCAMAAABhq6zVAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAJUExURUxpcf8AN////7f4NBoAAAABdFJOUwBA5thmAAAAMUlEQVQI103MAQ4AMAQEQev/j66i6YrEXIKIX9jY2NjYyDmhZnlCo5rdyWvebfYDVAcSmABbA7WD+QAAAABJRU5ErkJggg==);
}
.tb-key .tm-relate-list i {
  display: none;
}
.tb-prop li a:hover,
.tb-prop li.tb-selected a,
.tb-prop li.tb-selected a:hover,
.tm-bundle-dialog .bundle-items .bundle-item .tm-meta li.tb-selected a,
.tm-bundle-dialog .bundle-items .bundle-item .tm-meta li.tb-selected a:hover {
  border: 2px solid #ff0036 !important;
  margin: -1px;
}
.tb-key .tb-selected i {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 12px;
  height: 12px;
  overflow: hidden;
  text-indent: -99em;
  display: block;
  background-repeat: no-repeat;
  background-position: 0 0;
}
body {
  background: #fff !important;
}
.tb-gallery .tb-thumb li {
  display: inline-block;
  margin: 0 0 0 16px;
  padding-top: 22px;
}
.tb-gallery .tb-thumb img {
  position: relative;
  max-width: 60px;
  max-height: 60px;
}
.tb-gallery .tb-thumb .tb-selected img {
  left: -2px;
  top: -2px;
}
/deep/.el-input-number__decrease,
/deep/.el-input-number__increase {
  width: 20px;
}
/deep/.el-input-number.is-controls-right .el-input__inner {
  padding-left: 0px;
  padding-right: 20px;
}
.navigation-con {
  width: 100%;
  height: 45px;
  background: #333;
  position: relative;
  color: #fff;
  font-size: 14px;
  display: flex;
  justify-content: center;
  .navigation-bar {
    display: flex;
    width: 990px;
    justify-content: space-between;
    align-items: center;
    li {
      & a:hover {
        filter: progid:DXImageTransform.Microsoft.Alpha(opacity=65);
        opacity: 0.65;
        text-decoration: none;
        color: #fff;
        transition: all 0.5s linear;
      }
      .navigation-input {
        width: 138px;
        height: 19px;
        border-radius: 50px;
        border: 0;
        padding-left: 20px;
      }
      .navsearch-btn {
        border: none;
        width: 12px;
        height: 12px;
        cursor: pointer;
        position: absolute;
        top: 5px;
        left: 5px;
      }
    }
  }
}
#detail {
  width: 990px !important;
  margin: 20px auto;
  .tm-detail-meta {
    width: 990px;
    position: relative;
    z-index: 100;
    display: flex;
    min-height: 600px;
    .tb-gallery {
      width: 460px;
      position: relative;
      overflow: hidden;
      .tb-booth {
        position: relative;
        // background: url();
        display: table;
        table-layout: fixed;
        z-index: 1;
        width: 420px;
        height: 420px;
        margin: 20px auto 0;
        img {
          vertical-align: middle;
          width: 418px;
          height: 418px;
          border: 1px solid rgba(0, 0, 0, 0.05);
          border: 1px solid silver\9;
          display: table-cell;
          vertical-align: middle;
          text-align: center;
        }
      }
      .tb-thumb {
        display: flex;
        justify-content: space-evenly;
        text-align: center;
        white-space: nowrap;
        position: relative;
        transition: left 0.2s cubic-bezier(0, 0, 0.25, 1);
        font-size: 0;
        width: 420px;
        margin: 20px auto 0;
        .tb-selected a {
          border: 2px solid #000;
          width: 56px;
          height: 56px;
        }
        a {
          float: left;
          position: relative;
          width: 60px;
          height: 60px;
          overflow: hidden;
        }
      }
      .tm-action {
        display: flex;
        justify-content: space-between;
        padding: 38px 40px 25px;
        color: #999;
      }
    }
    .tb-property {
      flex: 1;
      .tb-detail-hd {
        padding: 20px 10px 12px;
        color: #000;
        h1 {
          padding-bottom: 0.2em;
          line-height: 1;
          font-size: 16px;
          font-weight: 700;
          font-family: "microsoft yahei";
          color: #000;
        }
      }
      .tm-fcs-panel {
        background-color: #e9e9e9;
        background-repeat: no-repeat;
        position: relative;
        left: 0;
        z-index: 10;
        font: 12px/1.5 "Microsoft Yahei", tahoma, arial;
        padding-top: 5px;
        margin-right: 20px;
        .tm-price-cur {
          line-height: 30px;
        }
        .tm-price-panel {
          position: static;
          color: #333;
          padding-left: 0;
          .tb-metatit {
            color: #999;
            font-size: 12px;
            text-align: left;
            float: left;
            width: 69px;
            margin: 0 0 0 8px;
          }
          .tm-yen {
            color: #ff0036;
            font-size: 18px;
          }
          .tm-price {
            color: #ff0036;
            font-size: 24px;
            font-weight: bolder;
          }
        }
        dd {
          color: #333;
          margin-left: 70px;
          font-family: Arial;
        }
      }
      .tm-ind-panel {
        border: 1px dotted #c9c9c9;
        border-width: 1px 0;
        margin-top: 5px !important;
        margin: -1px 20px 0 0;
        padding: 10px 0;
        position: relative;
        overflow: hidden;
        clear: both;
        display: flex;
        .tm-ind-item {
          float: left;
          width: 33%;
          text-align: center;
          position: relative;
          left: -1px;
          border-left: 1px solid #e5dfda;
          flex: 1;
          line-height: 16px;
        }
      }
      .tb-key {
        margin: 0 20px 24px 10px;
        .tb-skin {
          padding: 10px 0;
          .tb-sku {
            .tb-metatit {
              padding-top: 6px;
            }
            padding: 5px 0 12px;
            position: relative;
            .tb-prop {
              padding-bottom: 6px;
              li {
                float: left;
                position: relative;
                margin: 0 4px 4px 0;
                line-height: 28px;
                vertical-align: middle;
                padding: 1px;
                max-width: 95%;
              }
            }
          }
        }
      }
    }
  }
}

.goHome:hover {
  color: rgb(255, 0, 54);
  text-decoration: underline;
}
.tb-action {
  clear: both;
  padding: 10px 0 0 66px;
  margin: 10px 0 0;
}
.tb-btn-sku {
  margin-right: 10px;
  float: left;
}
#detail .tb-btn-basket {
  margin-right: 1px;
}
#detail .tb-sku .tm-relate-current span,
#detail .tb-sku a:hover {
  border: 2px solid #ff0036 !important;
  margin: -1px;
}
#detail .tb-sku .tm-relate-list .tm-relate-current i {
  display: block;
  position: absolute;
  bottom: 0;
  right: 0;
  width: 12px;
  height: 12px;
  overflow: hidden;
  text-indent: -99em;
  background-repeat: no-repeat;
  background-position: 0 0;
}

#detail .tb-sku .tm-relate-list .tm-relate-current i {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAwAAAAMCAMAAABhq6zVAAAABGdBT…v/j66i6YrEXIKIX9jY2NjYyDmhZnlCo5rdyWvebfYDVAcSmABbA7WD+QAAAABJRU5ErkJggg==);
}

.box:after,
.clear:after,
.clearfix:after,
.col-extra:after,
.col-sub:after,
.layout:after,
.main-wrap:after,
.tb-clearfix:after,
.tm-clear:after {
  content: "\20";
  display: block;
  height: 0;
  clear: both;
}
#detail .tm-relate-wrapper .tb-metatit {
  padding-top: 6px;
}
#detail .tb-metatit {
  text-align: left;
  float: left;
  width: 66px;
}
.tb-key .tb-metatit {
  color: #838383;
}
.tb-metatit,
.tb-metatit a {
  color: #999;
}
.tb-amount-widget .mui-amount-input {
  vertical-align: middle;
}
.tb-text {
  padding: 3px 2px 0 3px;
  line-height: 26px;
}
.tb-ex-select span,
.tb-text {
  font-size: 12px;
  margin: 0;
  height: 26px;
  border: 1px solid #a7a6ac;
  width: 36px;
  background-position: -406px -41px;
  color: #666;
}
.tb-amount-widget .mui-amount-btn {
  display: inline-block;
  vertical-align: middle;
}
.tm-delivery-panel .tb-postAge .tb-deliveryAdd {
  margin: 0 6px 0 0;
}
.tb-amount-widget .mui-amount-decrease {
  margin-top: 3px;
  transform: rotate(180deg);
}
.tm-delivery-panel {
  color: #333;
  position: relative;
}
.tm-delivery-panel .tb-postAge .tb-postAge-info {
  color: #333;
  padding: 0 5px 0 0;
  position: relative;
  display: inline-block;
}
.tb-amount-widget .mui-amount-decrease,
.tb-amount-widget .mui-amount-increase {
  width: 16px;
  height: 12px;
  overflow: hidden;
  border: 1px solid #a7a6ab;
  display: block;
  line-height: 12px;
  font-size: 5px;
  color: #666;
  justify-content: center;
  align-items: center;
  display: flex;
  cursor: pointer;
}
.tm-relate-list {
  overflow: hidden;
}
#detail .tb-sku .tm-relate-list li a,
#detail .tb-sku .tm-relate-list li span {
  display: block;
  white-space: nowrap;
  width: auto !important;
  min-width: 10px;
  max-width: 405px;
  padding: 0 6px 0 7px;
  text-align: center;
  border: 1px solid #e2e1e3;
  color: #000;
  text-decoration: none;
  overflow: hidden;
  text-overflow: ellipsis;
}
.tm-ind-emPointCount .tm-indcon .tm-count {
  color: #280;
}
#detail .tb-btn-sku a {
  margin-right: 0;
  float: left;
  overflow: hidden;
  position: relative;
  width: 178px;
  background-color: #ffeded;
  border: 1px solid #ff0036;
  color: #ff0036;
  font-family: "Microsoft Yahei";
}
#detail .tb-btn-add a,
#detail .tb-btn-basket a,
#detail .tb-btn-buycar a {
  background-color: #ff0036 !important;
  border: 1px solid #ff0036;
  color: #fff !important;
}
#detail .tb-meta {
  margin: 5px 20px 5px 0;
}

#detail .tb-meta dl {
  line-height: 24px;
}

#detail .tb-meta dl:after {
  content: " ";
  display: block;
  overflow: hidden;
  height: 0;
  font-size: 0;
  clear: both;
}

#detail .tb-meta dl .tb-metatit {
  color: #999;
  font-size: 12px;
  text-align: left;
  float: left;
  width: 50px;
  margin: 0 10px;
}

#detail .tb-meta dl dd {
  margin-left: 70px;
}

#detail .tb-meta dl dd .tb-cf60 {
  color: #f60;
}

#detail .tb-meta span#J_SSLIcon {
  width: auto;
}

#detail .tb-meta .tbid-indicator span {
  width: 72px;
}

.tm-promo-slider {
  background-color: #fafafa;
  border-top: 1px solid #f0f0f0;
  padding: 10px 20px 10px 86px;
  overflow: hidden;
  position: absolute;
  z-index: 1;
  width: 421px;
  left: 0;
  top: 100%;
  display: none;
  margin-left: -20px;
}

#detail .showList .tm-promo-slider {
  display: block;
}

#detail .tb-meta .tm-promo-slider li {
  margin-bottom: 10px;
  clear: both;
  height: 18px;
}

#detail .tm-promo-slider .price {
  color: #f60;
  font-size: 12px;
  font-weight: 400;
  font-family: Arial;
  background: 0 0;
  padding-left: 0;
}

#detail .tm-promo-slider .post-script {
  color: grey;
  padding: 5px 0 15px;
  clear: both;
}

#detail .tb-btn-sku a {
  margin-right: 0;
  float: left;
  overflow: hidden;
  position: relative;
  width: 178px;
  background-color: #ffeded;
  border: 1px solid #ff0036;
  color: #ff0036;
  font-family: "Microsoft Yahei";
}
#detail .tb-btn-sku a,
#detail .tm-change-left {
  height: 38px;
  line-height: 38px;
  text-align: center;
  font-size: 16px;
}
.tm-ind-item .tm-label,
.tm-ind-item .tm-monthavg {
  display: inline-block;
  line-height: 16px;
  height: 16px;
  color: #999;
}
.tm-ind-panel .tm-count {
  display: inline-block;
  line-height: 16px;
  height: 16px;
  color: #ff0036;
  font-weight: 700;
  margin-left: 3px;
}
#detail .tm-fcs-panel,
#detail .tm-fcs-panel dl.tm-shopPromo-panel .tm-floater-Box .fold .hd {
  background-image: url(data:image/png;base64,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);
}
.iconfont {
  font-size: inherit;
}
.tb-detail-hd h1 a,
.tb-detail-hd h3 a {
  vertical-align: middle;
  color: #000;
}
</style>