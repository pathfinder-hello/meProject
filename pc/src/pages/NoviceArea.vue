<template>
  <div class="noviceArea front" v-TDK="TDK">
    <div class="index-slider">
      <div class="index-slider-box">
        <div class='swiper-container'>
          <div class='swiper-wrapper'>
            <div class="swiper-slide front-banner" v-for="item in banners" :key='item.resLink'>
              <a :href="item.resLink || 'javascript:;'" target="_blank">
                <img :src="item.resUri" alt="">
              </a>
            </div>
          </div>
          <div class="pagination"></div>
        </div>
      </div>
    </div>

    <div class="container">

      <div class="section-space"></div>
      <div class="section-space"></div>

      <h4 class="section-title">聚寶進階</h4>

      <div class="product-area product-box front-new-novice-box">
        <div class="content">
          <div class="product-month xrt-row xrt-row-new-novice" style="border: none;">
            <div class="col-xs-4">
              <div class="front-new-user">
                <img src="/static/img/people.png" alt="" style="width: 70px;">
              </div>
              <p>註冊領1%加息券見面禮</p>
              <p class="product-noviceArea-desc" style="text-align: left;">註冊即可領取1%加息券，可為您獲取更高的投資回報。</p>
              <a class="front-new-user-reg new-user-active front-new-novice-reg" style="background: #f05a23;color: #fff;" v-if="isloging"  href="/coupon">查看禮券</a>
              <a class="front-new-user-reg new-user-active front-new-novice-reg" v-else @click="isLogin" href="javascript:;">註冊領取</a>
            </div>
            <div class="col-xs-4">
              <div class="front-new-user">
                <img src="/static/img/note.png" alt="" style="width: 70px;">
              </div>
              <p>測評送積分</p>
              <p class="product-noviceArea-desc">完成風險測評，享受安心出借。</p>
              <a class="front-new-user-reg new-user-active front-new-novice-reg" @click="getCurrentInfoMes" href="javascript:;">完成評測</a>
            </div>
            <div class="col-xs-4" style="border: none">
              <div class="front-new-user">
                <img src="/static/img/hand.png" alt="" style="width: 70px;">
              </div>
              <p>拿第壹桶金</p>
              <p class="product-noviceArea-desc" style="text-align: left;">首次出借新手專享項目，期待年回報率達6% 。</p>
              <a class="front-new-user-reg new-user-active front-new-novice-reg"  @click="toBucketDeatil" href="javascript:;">完成出借</a>
            </div>
          </div>
        </div>
      </div>

      <div class="section-space"></div>
      <div class="section-space"></div>

      <div class="noviceArea-parper">
        <div class="novice-img">
          <img src="/static/img/notice.svg" alt="" style="width:36px;height:32.8px;margin-right:10px;">
        </div>
        <div class="noviceArea-tit">聚寶快報</div>
        <div class="noviceArea-desc">聚寶盆發起「理財，我是保守派」，倡導積極健康財富觀</div>
      </div>

      <div class="section-space"></div>
      <div class="section-space"></div>

      <h4 class="section-title">聚寶秘笈</h4>
      <div class="noviceArea-video">
        <img style="width: 100%;" src="/static/img/friend.png" alt="">
      </div>

      <div class="section-space"></div>
      <div class="section-space"></div>
    </div>
  </div>
</template>

<script>
  import Swipe from 'swiper'

  export default {
    name: "novice-area",
    data() {
      return {
        banners:[],
        products: {
          30: {},
        },
        TDK: {
          title:'聚寶盆新手專區',
          keyWords:'聚寶盆收益,聚寶盆收費標準,聚寶盆利息,聚寶盆提領',
          description:'聚寶盆會員幫助中心幫您解決登錄註冊、帳戶資訊、匯款提領、產品介紹等壹系列問題‘，有問題找幫助中心，希望給您的預訂疑問提供幫助! 服務熱線 02-8780-6767 。',
        }
      }
    },
    computed:{
      isloging() {
        return sessionStorage.getItem('currentUser') && JSON.parse(sessionStorage.getItem('currentUser'))['cusMobile'] != null && this.$store.state.accountInfo.cusMobile ? true : false;
      }
    },
    created(){
      const self = this;
      // banner
      this.$http.post('/pbap-web/action/resource/query/bannerList', {
        pageIndex: 1,
        pageSize: 5,
        resModule: 4
      }).then((res) => {
        self.banners = res.body.respInfo.list.dataList;
        self.$nextTick(function () {
          self.mySwipe = new Swipe('.swiper-container', {
            loop: true,
            autoplay: 3000,
            pagination: '.pagination',
            paginationClickable: true
          })
          self.mySwipe.resizeFix()
        })
      });
      // 首頁產品 新手
      self.$http.post('/pbap-web/action/product/query/lastNewcomerPrd', {prdType: 30}).then((res) => {
        self.products[30] = res.body.respInfo.product || {};
        console.log(self.products[30])
      })
    },
    methods: {
      toBucketDeatil() {
        localStorage.setItem('proCode', this.products[30].prdCode);
        this.$router.push({path: 'bucketGold'});
      },
      isLogin(){
        const _isLogin = sessionStorage.getItem('currentUser') && JSON.parse(sessionStorage.getItem('currentUser'))['cusMobile'];
        if (_isLogin) {
          this.$store.commit('setModal', {
            type: 'alert',
            msg: '已登入',
            confirmText: '我知道了'
          });
          this.$store.commit('showModal');
        } else {
          this.$router.push('/register')
        }
      },
      getCurrentInfoMes () {
        const self = this;
        this.$http.post('/pbap-web/action/customer/query/custAuthInfo',{}).then((res) => {
          self.riskTest = res.body.respInfo.custInfo.riskTest;
          let riskTest = res.body.respInfo.custInfo.riskTest;
          self.$store.commit('setCurrentUserInfo', res.body.respInfo.custInfo)
          var _str = '';
          if (riskTest > 0) {
            if (riskTest < 28) {
              _str = '保守型的投资者'
            } else if (riskTest >= 28 && riskTest < 39) {
              _str = '稳健型的投资者'
            } else if (riskTest >= 39) {
              _str = '积极的投资者'
            }
            this.$store.commit('setModal', {
              type: 'alert',
              msg: '根據風險評測結果，您屬於:'+_str,
              confirmText: '我知道了'
            });
            this.$store.commit('showModal');
          } else if (riskTest == 0) {
            self.$router.push({path:'riskAssessment'});
          }
        })
      },
    }
  }
</script>
