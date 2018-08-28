# swipe-action-wepy

> 微信小程序框架wepy - 向左滑动删除插件, 支持自定义内容区

## Requirements
- wepy: "^1.5.2"

## Usage
#### install

``` sh
 npm install swipe-action-wepy --save
```

#### 父组件 XXXX.wepy

``` wpy
<template>
  <view class="shop-carts-product-content">
      <repeat for="{{cartList}}" key="id" data-index="ind" item="cart">
        <swipeDelete :swipeData.sync="cart"
                     data-index="{{ind}}"
                     @delItem.user="handleDelItem"
        >
          <view class="shop-carts-product-contain">
            <view class="list">list</view>
          </view>
        </swipeDelete>
      </repeat>
   </view>
</template>

<script>
  import wepy from 'wepy'
  import swipeDelete from 'swipe-action-wepy'

  export default class Index extends wepy.page {
    components = {
      swipeDelete: swipeDelete,
    }

   data = {
         cartList: [
           {id: 1, title: '购物车1', style: 0},
           {id: 2, title: '购物车2', style: 0},
           {id: 3, title: '购物车3', style: 0},
           {id: 4, title: '购物车4', style: 0},
         ]
       }

    methods = {
        // 滑动删除
        handleDelItem (itemData, cb) {
          let that = this
          wx.showModal({
            title: '',
            content: '确认是否移除？',
            confirmColor: 'rgb(247, 68, 97)',
            success: function(res) {
              if (res.confirm) {
                that.$invoke('swipeDelete', 'slideHideBtn')
              } else if (res.cancel) {
                that.$invoke('swipeDelete', 'slideHideBtn')
              }
            }
          })
        }
    }
  }
</script>
```
