<template>
  <el-aside width="180px" class="aside" ref="asideChange">
    <el-image class="headImg" ref="headImgChange" src="/static/img/logo.jpg" fit="contain"></el-image>
    <el-menu
      :collapse="fold"
      class="menu sele_none"
      :default-active="onRoutes"
      background-color="#fff"
      text-color="#000"
      active-text-color="#feaa30"
      unique-opened
      router
    >
      <template v-for="item in items">
        <template v-if="item.subs && item.subs.length > 0">
          <el-submenu :index="item.url" :key="item.index">
            <template slot="title">
              <i class="icon margin_r_20" :class="item.icon"></i>
              <span slot="title">{{ item.title }}</span>
            </template>
            <template v-for="subItem in item.subs">
              <el-menu-item :index="subItem.url" :key="subItem.index">{{ subItem.title }}</el-menu-item>
            </template>
          </el-submenu>
        </template>
        <template v-else>
          <el-menu-item :index="item.url" :key="item.index">
            <i class="icon margin_r_20" :class="item.icon"></i>
            <span slot="title">{{ item.title }}</span>
          </el-menu-item>
        </template>
      </template>
    </el-menu>
  </el-aside>
</template>

<script>
import bus from '@/common/bus'
export default {
  data() {
    return {
      fold: false,
      items: [],
      datas: [],
    }
  },
  methods: {
    getSubs(params) {
      let arr = this.datas.filter(x => x.module_parent_guid == params._id)
      let subs = []
      arr.forEach(data => {
        subs.push({
          index: 'sub_' + data._id,
          url: data.module_url || 'sub_' + data._id,
          title: data.module_name,
        })
      })

      return subs
    },
    getMenu() {
      const res = {
        code: 200,
        msg: '',
        datas: {
          authorize_modules: [
            {
              _id: '758a7f6c-f033-449e-b3c8-dca323c3e1f9',
              module_parent_guid: '',
              module_name: '系统首页',
              module_url: '/pages/home',
              module_icon: 'iconfont iconshouye01-01',
            },
            {
              _id: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_parent_guid: '',
              module_name: '店铺管理',
              module_url: '',
              module_icon: 'iconfont icondianpu',
            },
            {
              _id: '88fb4c51-cc31-4abe-abb4-46c67c4476b3',
              module_parent_guid: '',
              module_name: '商品管理',
              module_url: '',
              module_icon: 'iconfont iconchanpin',
            },
            {
              _id: '465b3efa-d5c2-4dce-808d-16c2aeddbe55',
              module_parent_guid: '',
              module_name: '订单管理',
              module_url: '',
              module_icon: 'iconfont iconquanbudingdan',
            },
            {
              _id: '3f853e04-eab3-4019-93fc-9478cda764c9',
              module_parent_guid: '',
              module_name: '会员管理',
              module_url: '',
              module_icon: 'iconfont iconyonghu',
            },
            {
              _id: '91a55a2c-335a-4c36-a9f5-5d1cea96132e',
              module_parent_guid: '',
              module_name: '应用管理',
              module_url: '',
              module_icon: 'iconfont iconyingyong',
            },
            {
              _id: 'f517cade-46ee-4735-9a1d-b48be2f9d1cc',
              module_parent_guid: '',
              module_name: '系统设置',
              module_url: '',
              module_icon: 'iconfont iconxitongshezhi',
            },
            {
              _id: 'f8bed44c-bb20-46d3-9b60-6e182540e8e8',
              module_parent_guid: '',
              module_name: '日志管理',
              module_url: '',
              module_icon: 'iconfont iconrizhi',
            },
            {
              _id: '06b7301b-e433-4429-9476-e93f3eff963c',
              module_parent_guid: '91a55a2c-335a-4c36-a9f5-5d1cea96132e',
              module_name: '小程序',
              module_url: '/pages/app/mp/mp_page',
              module_icon: '',
            },
            {
              _id: 'd9105323-15dc-43a2-9165-13d0f36f4c2a',
              module_parent_guid: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_name: '店铺首页',
              module_url: '/pages/shop/home/page',
              module_icon: '',
            },
            {
              _id: '5ade17a5-99d8-41fd-9ed3-0f2b832159f7',
              module_parent_guid: '88fb4c51-cc31-4abe-abb4-46c67c4476b3',
              module_name: '商品列表',
              module_url: '/pages/goods/list/goods_list',
              module_icon: '',
            },
            {
              _id: '5437d34a-3de2-4347-a893-3ffff57e2162',
              module_parent_guid: '3f853e04-eab3-4019-93fc-9478cda764c9',
              module_name: '会员列表',
              module_url: '/pages/member/list/member_list',
              module_icon: '',
            },
            {
              _id: '56b1109a-7db4-4c7a-a078-9d278586a7ac',
              module_parent_guid: '465b3efa-d5c2-4dce-808d-16c2aeddbe55',
              module_name: '订单列表',

              module_url: '/pages/order/order/order_list',
              module_icon: '',
            },
            {
              _id: '82b57c1b-d5fc-4c20-8a39-2a45a0c27542',
              module_parent_guid: 'f8bed44c-bb20-46d3-9b60-6e182540e8e8',
              module_name: '操作日志',
              module_url: '/pages/log/operation_log',
              module_icon: '',
            },
            {
              _id: '6f4f903a-77c1-454e-8943-7df6b5bf6ac8',
              module_parent_guid: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_name: '图文导航',
              module_url: '/pages/shop/graphic_classify/classify_navigation',
              module_icon: '',
            },
            {
              _id: '6f4f903a-77c1-454e-8943-7df6b5bf6ac9',
              module_parent_guid: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_name: '卡片导航',
              module_url: '/pages/shop/card_classify/classify_navigation',
              module_icon: '',
            },
            {
              _id: '4a248661-531c-429c-a513-031375572f9e',
              module_parent_guid: '88fb4c51-cc31-4abe-abb4-46c67c4476b3',
              module_name: '商品分类',
              module_url: '/pages/goods/classify/goods_classify',
              module_icon: '',
            },
            {
              _id: '4482135a-09c9-4b08-93e4-955e8c5e6314',
              module_parent_guid: 'f517cade-46ee-4735-9a1d-b48be2f9d1cc',
              module_name: '账号管理',
              module_url: '/pages/system_set/account/account',
              module_icon: '',
            },
            {
              _id: '6a3c2b73-c69a-484b-8894-8976bde06350',
              module_parent_guid: '465b3efa-d5c2-4dce-808d-16c2aeddbe55',
              module_name: '退款处理',
              module_url: '/pages/order/refunds_dispose',
              module_icon: '',
            },
            {
              _id: '63dad488-27dc-4711-8d2b-b6b8a9f6fe04',
              module_parent_guid: '88fb4c51-cc31-4abe-abb4-46c67c4476b3',
              module_name: '标签管理',
              module_url: '/pages/goods/label/page',
              module_icon: '',
            },
            {
              _id: '8006f8db-f724-453e-bf91-7c5e5a2daf95',
              module_parent_guid: 'f517cade-46ee-4735-9a1d-b48be2f9d1cc',
              module_name: '角色管理',
              module_url: '/pages/system_set/role/role',
              module_icon: '',
            },
            {
              _id: '4443db8b-5597-4d25-a508-6c52f312d007',
              module_parent_guid: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_name: '限时精选',
              module_url: '/pages/shop/limit',
              module_icon: '',
            },
            {
              _id: 'd6626496-5d0e-4d97-871f-8efe964505f8',
              module_parent_guid: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_name: '热门推荐',
              module_url: '/pages/shop/hot',
              module_icon: '',
            },
            {
              _id: '400f5055-c1c6-456f-a3cf-69349036df05',
              module_parent_guid: '88fb4c51-cc31-4abe-abb4-46c67c4476b3',
              module_name: '商品评价',
              module_url: '/pages/goods/evaluate',
              module_icon: '',
            },
            {
              _id: 'f12276ee-fb94-4e9e-942c-bab97e789c0a',
              module_parent_guid: '0f15d115-c4b8-46a8-9469-b1c404aab6e6',
              module_name: '搜索管理',
              module_url: '/pages/shop/search/page',
              module_icon: '',
            },
            {
              _id: '9f7f2915-c9e3-4d04-a4c8-e9d649d2e0a8',
              module_parent_guid: '465b3efa-d5c2-4dce-808d-16c2aeddbe55',
              module_name: '交易设置',
              module_url: '/pages/order/deal_set',
              module_icon: '',
            },
          ],
        },
      }

      this.datas = res.datas.authorize_modules
      this.datas.forEach(data => {
        if (data.module_parent_guid == '')
          this.items.push({
            icon: data.module_icon,
            url: data.module_url || data._id + '',
            index: data._id + '',
            title: data.module_name,
            subs: this.getSubs(data),
          })
      })

      uni.setStorage({
        key: '__menu',
        data: this.datas,
      })
      return
      this.$axios.get('sys/module/authorize').then(res => {
        if (res.code == 200) {
          this.datas = res.datas.authorize_modules
          this.datas.forEach(data => {
            if (data.module_parent_guid == '')
              this.items.push({
                icon: data.module_icon,
                url: data.module_url || data._id + '',
                index: data._id + '',
                title: data.module_name,
                subs: this.getSubs(data),
              })
          })
        }
      })
    },
  },
  created() {
    bus.$on('fold', res => {
      this.fold = res
      if (res) {
        this.$refs.asideChange.$el.style.width = '64px'
        this.$refs.headImgChange.$el.style.width = '64px'
        this.$refs.headImgChange.$el.style.height = '100px'
      } else {
        this.$refs.asideChange.$el.style.width = '180px'
        this.$refs.headImgChange.$el.style.width = '100%'
        this.$refs.headImgChange.$el.style.height = '100px'
      }
    })

    this.items = []

    if (this.items.length <= 0) {
      this.getMenu()
    }
  },
  computed: {
    onRoutes() {
      return this.$route.path
    },
  },
}
</script>

<style>
>>> .el-menu {
  border: none;
}

>>> .el-submenu__title:hover,
>>> .el-menu-item:hover,
>>> .el-submenu__title:hover i {
  color: #feaa30 !important;
  background-color: #fff !important;
}

>>> .el-submenu__icon-arrow {
  top: 31px;
  right: 20px;
  transform: rotate(-90deg);
}

>>> .el-submenu.is-opened > .el-submenu__title .el-submenu__icon-arrow {
  transform: rotate(0deg);
}

>>> .el-submenu .el-menu-item {
  min-width: initial !important;
  padding: 0 0 0 68px !important;
}

>>> .el-menu-item i {
  color: #909399;
}

>>> .el-menu-item.is-active::after {
  position: absolute;
  top: 50%;
  right: 0;
  width: 0.3125rem;
  height: 1.25rem;
  background-color: #feaa30;
  content: ' ';
  transform: translate(0, -50%);
}

.aside {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  overflow-x: hidden;
  overflow-y: hidden;
  background-color: #fff;
  transition: all 0.3s ease-in-out;
}

.headImg {
  width: 100%;
  height: 100px;
  transition: all 0.3s ease-in-out;
}

.menu {
  height: calc(100% - 100px);
  overflow: auto;
  overflow-x: hidden;
}

.main::-webkit-scrollbar {
  display: none;
}

.icon {
  font-size: 20px;
}
</style>
