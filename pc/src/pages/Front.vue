<template>
  <div class="front">
    <div id="inAd" v-if="inAd">
      <div class="modal-backdrop fade in" @click="inAd = !inAd"></div>
      <div class="ad-content text-center" @click="inAd = !inAd">
        <a :href="adData.popLink" id="adImgBox" target="_blank">
          <img id="adImg" class="img-responsive" alt="活動" :src="adData.popUri">
        </a>
        <div class="close" style="opacity:1;">
          <img src="/static/img/close-btn.png" alt="關閉">
        </div>
      </div>
    </div>
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
    <div style="background-color:#fff;">
      <div class="website-info" style="width: 1080px !important;margin: 0 auto;border-bottom: 1px solid #d9d9d9;">
        <!--<div class="numbers">
            <div class="title">信融通平臺</div>
            <div class="service-date">平穩運營<span>{{webSiteInfo.operateDay}}</span>天</div>
            <div class="service-date">累計投資金額<span>{{webSiteInfo.investmentAmount}}</span>元</div>
            <div class="service-date">累計註冊人數達<span>{{$fmoneyFormat(webSiteInfo.investmentCount)}}</span>人</div>
            <div class="service-date">累計賺取<span>{{webSiteInfo.income}}</span>元</div>
        </div>-->

        <div class="website-intro">
          <div class="info info1">
            <img src="/static/img/newUser.png">
            <p class="info-top">優選產品 服務多元</p>
            <p class="info-desc">提供多種投資理財服務， </p>
            <p class="info-desc">產品豐富、期限多樣 </p>
          </div>
          <div class="info info2" style="padding-right: 20px;padding-left: 30px;">
            <img src="/static/img/shezhi.png">
            <p class="info-top">多重風控 安全保障</p>
            <p class="info-desc">產品層層篩選，保證用戶資金安全</p>
            <p class="info-desc">借款人資質經三重審核</p>
          </div>
          <div class="info info3">
            <img src="/static/img/tuijian.png">
            <p class="info-top">一鍵投資 操作簡單</p>
            <p class="info-desc">7×24小時在線下單</p>
            <p class="info-desc">資金不放假，回款有規劃</p>
          </div>
          <!--<div class="info info1"><i class="icon icon-select"></i>嚴格甄選 優質產品</div>-->
          <!--<div class="info info2"><i class="icon icon-six"></i>六層風控 安全保障</div>
          <div class="info info3"><i class="icon icon-service"></i>貼心服務 便捷流程</div>-->
        </div>
      </div>
      <div class="info-notice" style="width: 1080px !important;margin: 0 auto;padding-left: 0px;">
        <div class="pull-left title">
          <img src="/static/img/notice.svg" style="width:36px;height: 32.8px;">
          <!--<span>平臺公告</span>-->
        </div>
        <div class="notice-content">
          <ul class="list-unstyled" style="position: relative; margin-left: 0px;" id="newsLoad3">
            <li>
              <a :href="'/notice/'+notice.newsId" target="_blank">{{notice.newsTitle}}</a>
              <span class="" style="padding-left: 20px; color: #999;">{{notice.newsTime}}</span>
            </li>
          </ul>
        </div>
        <div class="gongg">
          <a class="pull-right text-muted more img-bg" href="/notice-list" target="_blank"></a>
          <a class="pull-right text-muted more" href="/notice-list" target="_blank" style="padding-right:10px;">更多公告</a>
          <!--<img src="/static/img/more_1.png" style="width: auto;height: 16px;position: absolute;top:0px;">-->

        </div>
      </div>
    </div>
    <div class="container">

      <div class="section-space"></div>
      <div class="section-space"></div>

      <h4 class="section-title">新手專區
        <div class="section-title-text">
          新手出借指南
        </div>
        <div class="gongg" style="display: inline;">
          <a class="pull-right text-muted more img-bg" href="/noviceArea" target="_blank"
             style="top: -4px;margin-left:8px;"></a>
          <a class="pull-right text-muted more" href="/noviceArea" target="_blank">查看更多</a>
        </div>
      </h4>
      <!--<h4 class="section-title">聚寶進階</h4>-->

      <div class="product-area product-box front-new-novice-box">
        <div class="content">
          <div class="product-month xrt-row xrt-row-new-novice" style="border: none;">
            <div class="col-xs-4">
              <div class="front-new-user">
                <img src="/static/img/people.png" alt="" style="width: 70px;">
              </div>
              <p>註冊領1%加息券見面禮</p>
              <p class="product-noviceArea-desc" style="text-align: left;">註冊即可領取1%加息券，可為您獲取更高的投資回報。 </p>
              <a class="front-new-user-reg new-user-active front-new-novice-reg" style="background: #f05a23;color: #fff;" v-if="isloging"  href="/coupon">查看禮券</a>
              <a class="front-new-user-reg new-user-active front-new-novice-reg" v-else @click="isLogin" href="javascript:;">註冊領取</a>
            </div>
            <div class="col-xs-4">
              <div class="front-new-user">
                <img src="/static/img/note.png" alt="" style="width: 70px;">
              </div>
              <p>測評送積分</p>
              <p class="product-noviceArea-desc">完成風險測評，享受安心出借。</p>
              <a @click="toRisk" class="front-new-user-reg new-user-active front-new-novice-reg" href="javascript:;">完成評測</a>
            </div>
            <div class="col-xs-4" style="border: none">
              <div class="front-new-user">
                <img src="/static/img/hand.png" alt="" style="width: 70px;">
              </div>
              <p>拿第壹桶金</p>
              <p class="product-noviceArea-desc" style="text-align: left;">首次出借新手專享項目，期待年回報率達6% 。</p>
              <div class="front-new-user-reg new-user-active front-new-novice-reg" @click="toBucketDeatil" style="cursor: pointer;">完成出借</div>
            </div>
          </div>
        </div>
      </div>

      <!--<div class="product-area product-box front-new-user-box">
        <div class="content">
          <div class="product-month xrt-row xrt-row-new-user" style="border: none;">
            <div class="col-xs-4">
              <div class="front-new-user">
                <img src="/static/img/select-03.png" alt="">
              </div>
              <p>注冊領獎金</p>
              <a class="front-new-user-reg new-user-active" href="/register">注冊領取新手獎金</a>
            </div>
            <div class="col-xs-4">
              <div class="front-new-user">
                <img src="/static/img/select-03.png" alt="">
              </div>
              <p>風險評測</p>
              <div class="front-new-user-reg">完成評測拿十積分</div>
            </div>
            <div class="col-xs-4" style="border: none">
              <div class="front-new-user">
                <img src="/static/img/select-03.png" alt="">
              </div>
              <p>新手專享</p>
              <div class="front-new-user-reg">新手出售專享10%</div>
            </div>
          </div>
        </div>
      </div>-->

      <div class="section-space clearfix"></div>
      <div class="section-space clearfix"></div>

      <h4 class="section-title">壹桶金 新手投資
        <div class="section-title-text">
          專享通道
        </div>
        <div class="gongg" style="display: inline;">
          <a class="pull-right text-muted more img-bg" href="/product-list/30/11/1" target="_blank"
             style="top: -4px;margin-left:8px;"></a>
          <a class="pull-right text-muted more" href="/product-list/30/11/1" target="_blank">查看更多</a>
        </div>
      </h4>

      <div class="product-area product-box">
        <div class="content">
          <div class="product-month xrt-row" style="border: none;">
            <div class="col-xs-3">
              <div class="text-danger default-rate">
                <span class="num">{{$fmoney(formatNum(products[30].defaultRate || 0, 100), 1)}}</span>%
                <span
                  v-if="products[30].rewardRate">+{{$fmoney(formatNum(products[30].rewardRate || 0, 100), 1)}}%</span>
              </div>
              <p class="text-muted text-small">預期年化收益</p>
            </div>
            <div class="col-xs-3">
              <div class="day">
                <p><span class="num">{{products[30].prdPeriod}}</span>天</p>
              </div>
              <p class="text-muted text-small">借款期限</p>
            </div>
            <div class="progress-area col-xs-6">
              <div class="progress-box pull-left">
                <!--<div class="text-warning">{{products[30].minInvAmt}}元起投</div>-->
                <div class="progress">
                  <div class="progress-bar progress-bar-warning"
                       :style="{'width':products[30].colPercent+'%'}"></div>
                </div>
              </div>
              <div class="pull-left progress-text" style="width: 40px;">{{products[30].colPercent}}%</div>
              <a class="btn btn-warning product-link set-margin" target="_blank" @click="toBucketDeatil"
                 href="javascript:;"
                 :class="{'gray':!(products[30].status == 11 || products[30].status == 12)}">
                {{products[30].status == 11 || products[30].status == 12 ? '立即加入' : '查看詳情'}}
              </a>
            </div>
          </div>
        </div>
      </div>

      <!--<div class="product-area product-new clearfix">
        <img src="/static/img/index-red.png" style="width: 320px; float: left;">
        &lt;!&ndash;<div class="pull-left product-title">
          <h4>註冊即得</h4>
          <p>新手必選，僅有壹次投資機會</p>
          <img src="/static/img/home_line.png" class="line">
          <img src="/static/img/index_bg2.png" class="bg">
          <p>新手專屬，隨時待命</p>
        </div>&ndash;&gt;
        <div class="content">
          <div class="row xrt-row">
            <div class="col-xs-4">
              <div class="term">

                <div><span
                  class="text-danger num">{{$fmoney(formatNum(products[30].defaultRate || 0, 100), 1)}}</span>
                  <span class="text-danger">%</span>
                  <span class="text-danger"
                        v-if="products[30].rewardRate">+{{$fmoney(formatNum(products[30].rewardRate || 0, 100), 1)}}%</span>
                </div>
                <div>預期年化收益</div>
              </div>
              &lt;!&ndash;<div class="progress-box">
                  <div class="text-warning">{{products[30].minInvAmt}}元起投</div>
                  <div class="progress">
                      <div class="progress-bar progress-bar-warning" :style="{'width':products[30].colPercent+'%'}"></div>
                  </div>
              </div>
              <div class="pull-right progress-text">
                  {{products[30].colPercent || '0'}}%
              </div>&ndash;&gt;
            </div>
            <div class="col-xs-4">
              <div class="day">
                <div><span class="num">{{products[30].prdPeriod}}</span>天</div>
                <div>借款期限</div>
              </div>

            </div>
            <div class="col-xs-4" style="border: none;">
              <div><span class="num" v-if='products[30].maxInvAmt'>{{$fmoneyFormat(products[30].maxInvAmt)}}</span>
                <span class="num" v-if='!(products[30].maxInvAmt)'>{{$fmoneyFormat(products[30].prdAmount)}}</span>元
              </div>
              <div>最高可投</div>
            </div>
          </div>
          <div class="row">
            <a class="xrt-btn limit-btn">限時發布</a>
            <a class="product-link xrt-btn btn-warning" target="_blank" style="float: right;"
               :href="products[30].prdCode?'/product/'+products[30].prdCode:'javascript:;'"
               :class="{'gray':!(products[30].status == 11 || products[30].status == 12)}">
              {{products[30].status == 11 || products[30].status == 12 ? '立即加入' : '查看詳情'}}
            </a>
          </div>
        </div>
      </div>-->

      <div class="section-space clearfix"></div>
      <div class="section-space clearfix"></div>


      <h4 class="section-title">聚寶計劃
        <div class="section-title-text">
          循環出借 分散投標
        </div>
        <div class="gongg" style="display: inline;">
          <a class="pull-right text-muted more img-bg" href="/product-list/7/11/1" target="_blank"
             style="top: -4px;margin-left:8px;"></a>
          <a class="pull-right text-muted more" href="/product-list/7/11/1" target="_blank">查看更多</a>
        </div>
      </h4>
      <div class="product-area product-box front-bg">
        <div class="plan-container">
          <!--<div class="product-month xrt-row" style="border: none;">
            <div class="col-xs-3">
              <div class="text-danger default-rate">
                <span class="num">{{$fmoney(formatNum(products[7].defaultRate || 0, 100), 1)}}</span>%
                <span v-if="products[7].rewardRate">+{{$fmoney(formatNum(products[7].rewardRate || 0, 100), 1)}}%</span>
              </div>
              <p class="text-muted text-small">預期年化收益</p>
            </div>
            <div class="col-xs-3">
              <div class="day">
                <p><span class="num">{{products[7].prdPeriod}}</span>天</p>
              </div>
              <p class="text-muted text-small">借款期限</p>
            </div>
            <div class="progress-area col-xs-6">
              <div class="progress-box pull-left">
                &lt;!&ndash;<div class="text-warning">{{products[7].minInvAmt}}元起投</div>&ndash;&gt;
                <div class="progress">
                  <div class="progress-bar progress-bar-warning"
                       :style="{'width':products[7].colPercent+'%'}"></div>
                </div>
              </div>
              <div class="pull-left progress-text">{{products[7].colPercent}}%</div>
              <a class="btn btn-warning product-link set-margin" target="_blank"
                 :href="products[7].prdCode?'/product/'+products[7].prdCode:'javascript:;'"
                 :class="{'gray':!(products[7].status == 11 || products[7].status == 12)}">
                {{products[7].status == 11 || products[7].status == 12 ? '立即加入' : '查看詳情'}}
              </a>
            </div>
          </div>-->
          <div class="plan-case-item" v-for="(item, index) in juBaoArr" :key="index" v-if="index < 3">
            <div class="plan-case-item-t">
              <div class="plan-case-item-t-l">
                <p class="rate">{{item.defaultRate ? $fmoney(formatNum(item.defaultRate || 0, 100), 1) : '--'}}%<span v-if="item.rewardRate">+{{$fmoney(formatNum(item.rewardRate || 0, 100), 1)}}%</span></p>
                <p class="desc">預期年化收益</p>
              </div>
              <div class="plan-case-item-t-m"></div>
              <div class="plan-case-item-t-r">
                <p class="date">{{item.prdPeriod ? item.prdPeriod : '---'}}天</p>
                <p class="desc">借款期限</p>
              </div>
            </div>
            <div class="plan-case-item-b" @click="toDetail(item.prdCode)">
              {{item.status == 11 || item.status == 12 ? '立即加入' : '查看詳情'}}
            </div>
          </div>
        </div>
      </div>

      <div class="section-space clearfix"></div>
      <div class="section-space clearfix"></div>


      <h4 class="section-title">分期投
        <div class="section-title-text">
          定期投資 分散投標
        </div>
        <div class="gongg" style="display: inline;">
          <a class="pull-right text-muted more img-bg" href="/product-list/30/11/1" target="_blank"
             style="top: -4px;margin-left:8px;"></a>
          <a class="pull-right text-muted more" href="/product-list/8/11/1" target="_blank">查看更多</a>
        </div>
      </h4>
      <div class="product-area product-box">
        <div class="content">
          <div class="product-month xrt-row" style="border: none;">
            <div class="col-xs-3">
              <div class="text-danger default-rate">
                <span class="num">{{$fmoney(formatNum(products[8].defaultRate || 0, 100), 1)}}</span>%
                <span v-if="products[8].rewardRate">+{{$fmoney(formatNum(products[8].rewardRate || 0, 100), 1)}}%</span>
              </div>
              <p class="text-muted text-small">預期年化收益</p>
            </div>
            <div class="col-xs-3">
              <div class="day">
                <p><span class="num">{{products[8].prdPeriod}}</span>天</p>
              </div>
              <p class="text-muted text-small">借款期限</p>
            </div>
            <div class="progress-area col-xs-6">
              <div class="progress-box pull-left">
                <!--<div class="text-warning">{{products[8].minInvAmt}}元起投</div>-->
                <div class="progress">
                  <div class="progress-bar progress-bar-warning"
                       :style="{'width':products[8].colPercent+'%'}"></div>
                </div>
              </div>
              <div class="pull-left progress-text" style="width: 40px;">{{products[8].colPercent}}%</div>
              <a class="btn btn-warning product-link set-margin" target="_blank" @click="toDetail(products[8].prdCode)"
                 href="javascript:;"
                 :class="{'gray':!(products[8].status == 11 || products[8].status == 12)}">
                {{products[8].status == 11 || products[8].status == 12 ? '立即加入' : '查看詳情'}}
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="section-space clearfix"></div>
      <div class="section-space clearfix"></div>


      <h4 class="section-title">月月盈
        <div class="section-title-text">
          定期投資 分散投標
        </div>
        <div class="gongg" style="display: inline;">
          <a class="pull-right text-muted more img-bg" href="/product-list/30/11/1" target="_blank"
             style="top: -4px;margin-left:8px;"></a>
          <a class="pull-right text-muted more" href="/product-list/9/11/1" target="_blank">查看更多</a>
        </div>
      </h4>
      <div class="product-area product-box">
        <div class="content">
          <div class="product-month xrt-row" style="border: none;">
            <div class="col-xs-3">
              <div class="text-danger default-rate">
                <span class="num">{{$fmoney(formatNum(products[9].defaultRate || 0, 100), 1)}}</span>%
                <span v-if="products[9].rewardRate">+{{$fmoney(formatNum(products[9].rewardRate || 0, 100), 1)}}%</span>
              </div>
              <p class="text-muted text-small">預期年化收益</p>
            </div>
            <div class="col-xs-3">
              <div class="day">
                <p><span class="num">{{products[9].prdPeriod}}</span>天</p>
              </div>
              <p class="text-muted text-small">借款期限</p>
            </div>
            <div class="progress-area col-xs-6">
              <div class="progress-box pull-left">
                <!--<div class="text-warning">{{products[9].minInvAmt}}元起投</div>-->
                <div class="progress">
                  <div class="progress-bar progress-bar-warning"
                       :style="{'width':products[9].colPercent+'%'}"></div>
                </div>
              </div>
              <div class="pull-left progress-text" style="width: 40px;">{{products[9].colPercent}}%</div>
              <a class="btn btn-warning product-link set-margin" target="_blank"
                 href="javascript:;" @click="toDetail(products[9].prdCode)"
                 :class="{'gray':!(products[9].status == 11 || products[9].status == 12)}">
                {{products[9].status == 11 || products[9].status == 12 ? '立即加入' : '查看詳情'}}
              </a>
            </div>
          </div>
        </div>
      </div>
      <div class="section-space clearfix"></div>
      <div class="section-space"></div>
      <h4 class="section-title" >債權/散標
        <div class="section-title-text">
          自主投資 期限靈活
        </div>
        <div class="gongg" style="display: inline;">
          <a class="pull-right text-muted more img-bg" href="/product-list/10/11/1" target="_blank"
             style="top: -4px;margin-left:8px;"></a>
          <a class="pull-right text-muted more" href="/product-list/10/11/1" target="_blank">查看更多</a>
        </div>
      </h4>
      <div class="product-result" >
        <ul class="list-unstyled">
          <li class="list-bar list-title">
            <div class="list1">年利率</div>
            <div class="list2">借款標題</div>
            <div class="list3">期限</div>
            <div class="list4">金額</div>
            <div class="list5">投標進度</div>
            <div class="list6">操作</div>
          </li>
          <li class="list-bar product-bar" v-for="(item,ind) in productList" v-if="ind < 6"
              :class="{'product-bar-high':ind%2 == 0}" :key='item.prdCode'>
            <a :href="'/product/' + item.prdCode" target="_blank">
              <div class="list1 list-color"><span>{{$fmoney(formatNum(item.defaultRate || 0, 100), 1)}}</span>%</div>
              <div class="list1 list-color" v-if="item.rewardRate">+{{$fmoney(formatNum(item.rewardRate || 0, 100),
                1)}}%
              </div>
              <div class="list2" :title="item.prdName">{{item.prdName}}</div>
              <div class="list3"><span>{{item.prdPeriod}}</span>天</div>
              <div class="list4">{{$fmoneyFormat(item.prdAmount)}}元</div>
              <div class="list5">
                <div class="progress-area">
                  <div class="progress-box pull-left">
                    <div class="progress">
                      <div class="progress-bar progress-bar-warning"
                           :style="{'width':item.colPercent+'%'}"></div>
                    </div>
                  </div>
                  <div class="pull-right progress-text">{{item.colPercent || '0'}}%</div>
                </div>
              </div>
              <div class="list6" v-if="item.status == 11">募集中</div>
              <div class="list6" v-if="item.status == 12">預熱中</div>
              <div class="list6" v-if="item.status == 14">已滿額</div>
              <div class="list6" v-if="item.status == 16">已過期</div>
              <div class="list6" v-if="item.status == 20">還款中</div>
              <div class="list6" v-if="item.status == 30">已還款</div>
              <div class="list6" v-if="item.status == 50">其它狀態</div>
            </a>
          </li>
        </ul>
        <br>
        <br>
        <br>
      </div>
    </div>
  </div>
</template>

<script>
  import Swipe from 'swiper'

  export default {
    name: 'Front',
    data() {
      return {
        banners: [],
        webSiteInfo: {},
        notice: {},
        products: {
          30: {},
          7: {},
          8: {},
          9: {},
        },
        newsList: {},
        coupers: {},
        inAd: false,
        adData: {},
        productList: {},
        riskTest: '',
        juBaoArr:[],
      }
    },
    components: {},
    created() {
      var self = this;
      //浮層
      self.$http.post("/pbap-web/action/resource/query/actPopup?type=0", {}).then((res) => {
        self.adData = res.body.respInfo.actPopup;
        if (self.adData.popUri) {
          if (!self.getCookie('adShow') && self.adData.status) {
            self.inAd = true;
            var now = new Date();
            var tommorrow = new Date(now.getTime() + 1000 * 60 * 60 * 24);
            var exp = new Date(tommorrow.toLocaleDateString());
            self.setCookie('adShow', 'true', exp);
          }
        }
      })

      // banner
      self.$http.post('/pbap-web/action/resource/query/bannerList', {
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
      })
      // 公告
      self.$http.post('/pbap-web/action/news/query/lastNews', {newsType: 1, pageSize: 5, pageIndex: 1}).then((res) => {
        self.notice = res.body.respInfo.news;
      })
      // 交易數據
      self.$http.get('/pbap-web/action/statistics/query/tradesSumInfo').then((res) => {
        self.webSiteInfo = res.body.respInfo.sumInfo;
        self.webSiteInfo.investmentAmount = self.$fmoney(self.webSiteInfo.investmentAmount);
        self.webSiteInfo.income = self.$fmoney(self.webSiteInfo.income);
      })
      // 首頁產品 新手
      self.$http.post('/pbap-web/action/product/query/lastNewcomerPrd', {prdType: 30}).then((res) => {
        self.products[30] = res.body.respInfo.product || {};
        sessionStorage.setItem('proCode', this.products[30].prdCode);
        console.log(self.products[30])
      })
      //聚宝计划
      self.$http.post('/pbap-web/action/product/query/prdList', {
        pageSize:3,
        prdType:"7",
        status:"11",
        pageIndex:"1",
      }).then((res) => {
        self.juBaoArr = res.body.respInfo.prdList.dataList || {};
        if (res.body.respInfo.prdList.dataList.length < 3) {
          let _len = res.body.respInfo.prdList.dataList.length;
          for (let i = 0; i < 3-_len; i++) {
            self.juBaoArr.push({});
          }
        }
      });
      self.$http.post('/pbap-web/action/product/query/lastHomePrd?8', {typeArr: [8], visibleTerm: 2}).then((res) => {
        self.products[8] = res.body.respInfo.product[0] || {};
      })
      self.$http.post('/pbap-web/action/product/query/lastHomePrd?9', {typeArr: [9], visibleTerm: 2}).then((res) => {
        self.products[9] = res.body.respInfo.product[0] || {};
      })
      self.$http.post('/pbap-web/action/product/query/prdList', {
        pageSize: 4,
        prdType: null,
        status: 11,
        pageIndex: 1,
        prdNature: 1
      }).then((res) => {
        self.productList = res.body.respInfo.prdList.dataList || {};
      })

      /*// 新聞
      self.$http.post('/pbap-web/action/news/query/newsList', {newsType: 0, pageSize: 4, pageIndex: 1}).then((res) => {
        self.newsList = res.body.respInfo.list.dataList;
      })
      // 合作夥伴
      self.$http.post('/pbap-web/action/cooperators/query/cooperators/1', {}).then((res) => {
        self.coupers = res.body.respInfo.coopList;
      })*/
      // this.getCurrentInfoMes();
    },
    mounted() {
      var self = this


      /*setTimeout(function () {
        self.couperSlider = new Swipe('.swiper-cooper', {
          loop: self.coupers.length > 6,
          autoplay: 3000,
          slidesPerView: 6,
          paginationClickable: true
        })
        self.couperSlider.resizeFix()
      })*/
    },
    computed:{
      isloging() {
        return sessionStorage.getItem('currentUser') && JSON.parse(sessionStorage.getItem('currentUser'))['cusMobile'] != null ? true : false;
      }
    },
    methods: {
      couperSliderPre() {
        var self = this
        self.couperSlider.swipePrev();
      },
      couperSliderNext() {
        var self = this
        self.couperSlider.swipeNext()
      },
      formatNum(val, cus) {
        var self = this
        return self.$formatNum(val, cus);
      },
      cutNewsContent(str) {
        var divEl = document.createElement('div')
        divEl.innerHTML = str;
        return divEl.innerText.substring(0, 48)
      },
      toDetail(code) {
        const _proCode = code;
        sessionStorage.setItem('proCode', _proCode);
        // _proCode && this.$router.push({name: 'Product', params: {prdCode: _proCode}});
        _proCode && this.$router.push({path: 'bucketGold'});
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
      toRisk() {
        this.getCurrentInfoMes()
      },
      toBucketDeatil() {
        this.$router.push({path: 'bucketGold'});
      },
      isLogin(){
        this.$router.push('/register')
      }
    }
  }
</script>

