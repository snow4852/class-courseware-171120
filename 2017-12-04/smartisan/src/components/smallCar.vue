<template>
  <div>
    <a href="javascript:;">购物车</a>
    <!--根据class改变颜色-->
    <span class="cart-empty-num cart-num">
      <i>0</i>
    </span>
    <div class="nav-cart-wrapper">
      <div class="nav-cart-list">
        <div class="empty" v-show="!shops.length">
          <h3>购物车为空</h3>
          <p>您还没有选购任何商品，现在前往商城选购吧!</p>
        </div>
        <div class="full" v-show="shops.length">
          <div class="nav-cart-items">
            <ul>
              <li class="clear" v-for="item in shops">
                <div class="cart-item js-cart-item cart-item-sell">
                  <div class="cart-item-inner">
                    <div class="item-thumb">
                      <img :src="item.shop_info.ali_image">
                    </div>
                    <div class="item-desc">
                      <div class="cart-cell">
                        <h4>
                          <a href="#/item/100027401">{{item.shop_info.title}}</a>
                        </h4>
                        <p class="attrs">
                          <span v-for="spec in item.shop_info.spec_json">{{spec.show_name}}</span>
                        </p>
                        <h6>
                          <span class="price-icon">¥</span>
                          <span class="price-num">{{item.price}}</span>
                          <span class="item-num">x {{item.count}}</span>
                        </h6>
                      </div>
                    </div>
                    <div class="del-btn" @click="remove(item.id)">删除</div>
                  </div>
                </div>
              </li>
            </ul>
          </div>
          <div class="nav-cart-total">
            <p>共 <strong class="ng-binding">{{totalCountAndMoney.totalCount}}</strong> 件商品</p>
            <h5>合计：<span class="price-icon">¥</span>
              <span class="price-num ng-binding" ng-bind="cartMenu.totalPrice">
                {{totalCountAndMoney.totalMoney}}
              </span>
            </h5>
            <h6>
              <router-link class="nav-cart-btn" :to="{name:'Car'}">
                去购物车
              </router-link>
            </h6>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

  export default {
    computed: {
      shops () {
        return this.$store.state.carShops
      },
      totalCountAndMoney () {
        // 从getter中取值
        return this.$store.getters.totalCountAndMoney
      }
    },
    methods: {
      remove (skuId) {
        this.$store.dispatch('removeCountAction', {skuId})
      }
    }
  }
</script>
