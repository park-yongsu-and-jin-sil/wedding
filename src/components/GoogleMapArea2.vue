<template>
  <div class="map">
    <div class="title_area _english_font _big_text _black">
      Location
    </div>
    <div class="_big_text _black">
      <b>오시는 길</b>
    </div>

    <div class="address_area _large_text _gray">
      {{  address }}<br>
      {{  locationName }}<br>
      <p>{{ locationPhoneNumber }}</p>
    </div>

    <a style="cursor: pointer" @click="copyAddress">
      <img class="addr_btn" src="../assets/images/new/map/aadr_btn.png" />
    </a>

    <div class="bottom center ui toast-container _toast" v-show="showCopyCompleteModal">
      <div class="floating toast-box" style="text-align: left">
        <div role="alert" class="ui toast compact _toast_color" style="opacity: 1;">
          <i class="copy icon" style="visibility: visible;"></i>
          <div class="content">
            <div class="message">복사가 완료되었습니다.</div>
          </div>
        </div>
      </div>
    </div>



    <iframe
        class="_google_map_iframe"
        :src="googleMapSrc"
        allowFullScreen="" loading="lazy"
        referrerPolicy="no-referrer-when-downgrade">
    </iframe>

    <div class="util_btn_icon_area">
      <a :href="navermapUrl">
        <img class="util_btn_icon" src="../assets/images/new/map/navermap.png"/>
      </a>
      <a :href="kakaoTaxiUrl">
        <img class="util_btn_icon" src="../assets/images/new/map/kakaonavi.png"/>
      </a>
      <a :href="tmapUrl">
        <img class="util_btn_icon" src="../assets/images/new/map/tmap.png"/>
      </a>
    </div>

    <div class="map_desc_area _tiny_text _gray">
      <p class="_large_text _green"><b>자가용</b></p>
      <Divider3 :padding-bottom="0" padding-right="44"/>
      <strong class="_small_text _black">서울/영등포 방면</strong><br>
      시흥대로(안양 방면 직진) > 안양대교 > 안양역 > 만안구청 사거리 직진<br>
      > 웨딩그룹위더스 안양 (우측 위치)<br>
      <br>
      <strong class="_small_text _black">수원/군포 방면</strong><br>
      1번 국도(서울 방면 직진) > 명학역 사거리 지나서 바로 우측<br>
      > 웨딩그룹위더스 안양<br>
    </div>

    <div class="map_desc_area _tiny_text _gray">
      <p class="_large_text _green"><b>지하철</b></p>
      <Divider3 :padding-bottom="0" padding-right="44"/>
      <strong class="_small_text _black">1호선 명학역 1번 출구 출구에서 도보 2분 거리 (약 150m 직진)</strong><br>
      ※ 별도의 셔틀버스는 운행하지 않습니다.
    </div>

    <div class="map_desc_area _tiny_text _gray">
      <p class="_large_text _green"><b>버스</b></p>
      <Divider3 :padding-bottom="0" padding-right="44"/>
      <strong class="_small_text _black">만안구청 하차 (도보 1분)</strong><br>
      일반: 1, 1-2, 5, 8-2, 11-2, 15, 15-2, 20, 31-7, 32, 35, 88, 350<br>
      좌석: 900<br>
      마을: 10-1, 10-2
    </div>
  </div>
</template>

<script>

import Divider3 from "@/components/Divider3.vue";

export default {
  name: "google-map-area",
  components : {
    Divider3
  },
  data() {
    return {
      locationName: "웨딩그룹위더스 안양",
      address : "경기 안양시 만안구 안양로 104",
      locationPhoneNumber: "T. 0507-1494-6605",
      showCopyCompleteModal: false,
      tmapUrl: "",
      kakaoTaxiUrl: "",
      navermapUrl: "",
      kakaomapUrl: "",
      googleMapSrc: "https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3170.224690962431!2d126.93142507602819!3d37.38451823454417!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x357b672ad7606121%3A0x3935e905e7f24f7c!2z7Juo65Sp6re466O57JyE642U7IqkIOyViOyWkQ!5e0!3m2!1sen!2skr!4v1770534778121!5m2!1sen!2skr",
    }
  },
  mounted() {
    this.makeUrls()
  },
  methods: {
    makeUrls() {
      const locationName = this.locationName
      this.tmapUrl = "tmap://search?name=" + locationName
      this.kakaoTaxiUrl = "https://t.kakao.com/launch?type=taxi&dest_lat=37.384514&dest_lng=126.934&ref=localweb"
      this.navermapUrl = "nmap://search?query=" + locationName
      this.kakaomapUrl = "kakaomap://search?q=" + locationName
    },
    copyAddress() {
      this.$copyText(this.address).then(() => {
        this.showCopyCompleteModal = true
        setTimeout(() => {
          this.showCopyCompleteModal = false
        }, 1000)
      })
    }
  }
};
</script>

<style lang="scss" scoped>

.map {
  margin-top: 18px;
  margin-bottom: 18px;
  text-align: center;
}

.title_area {
  margin-top: 56px;
  line-height: 24px;
  color: #797979;
  margin-bottom: 8px;
}


.address_area {
  margin-top: 16px;
  line-height: 30px;
  p {
    margin-top: 4px;
  }
}

.addr_btn {
  width: 82px;
  height: 44px;
  margin-top: 24px;
  line-height: 28px;
  margin-bottom: 48px;
}

._toast {
  bottom: 300px!important;
}

._toast_color {
  background-color: #4d7846!important;
  opacity: 0.9!important;
  color: white!important;
}

._google_map_iframe {
  margin-left: 10px;
  margin-right: 10px;
  border: 0;
  width: 80%;
  min-height: 310px;
  min-width: 320px;
}

.util_btn_icon_area {
  margin-top: 16px;
}

.util_btn_icon {
  width: 113px;
  height: 46px;
  background: var(--secondary-bg-color);
}

.map_desc_area {
  text-align: left;
  margin-top: 56px;
  margin-left: 43px;
  line-height: 28px;
}

</style>
