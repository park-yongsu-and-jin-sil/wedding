<template>
  <div class="invitation_area">
    <p class="header _big_text _green">
      <strong>♥️</strong><br />
    </p>
    <div class="desc _large_text _gray">
      저희 두 사람이 사랑과 믿음으로<br />
      한 가정을 이루게 되었습니다.<br />
      바쁘시더라도 부디 오셔서 저희들의 앞날을<br />
      축복해 주시고 격려해 주시면<br />
      더없는 기쁨이 되겠습니다.
    </div>

    <Divider3 :padding-bottom="0" padding-right="24" padding-left="24"/>

    <div class="names _small_text _gray">
      <span class="parents">{{ male.parents }}</span>
      <span class="sub">의 {{ male.sub }}</span>
      <strong class="name">
        <span v-for="char in male.name" :key="char">{{ char }}</span>
      </strong>

      <span class="parents">{{ female.parents }}</span>
      <span class="sub">의 {{ female.sub }}</span>
      <strong class="name">
        <span v-for="char in female.name" :key="char">{{ char }}</span>
      </strong>
    </div>

<!--    <div class="invi_main_blank"></div>-->
    <img class="invi_main_image" src="../assets/images/new/invitation/invi_img.png" />

  </div>
</template>

<script>

import Divider3 from "@/components/Divider3.vue";

export default {
  name: "invitation-area",
  components: {
    Divider3,
  },
  data() {
    return {
      male: {
        parents: "(故)박복식 · 신미애",
        sub: "장남",
        name: "박용수"
      },
      female: {
        parents: "(故)진광훈 · 김복여",
        sub: "장녀",
        name: "진실"
      },
    };
  },
  methods: {
  },
};
</script>

<style lang="scss" scoped>
.invitation_area {
  background: var(--secondary-bg-color);
  text-align: center;
  line-height: 0;
  .header {
    padding-top: 56px;
    line-height: 28px;
  }
  .desc {
    line-height: 30px;
    padding-bottom: 36px;
  }
  .line_area {
    padding-bottom: 36px;
  }
  .line {
    width: 382px;
    border: 0.7px solid;
    color: #D7D7D7;
  }
  .names {
    margin-top: 24px;
    padding-right: 68px;

    // 1층, 2층 상관없이 세로 칸을 일치시킵니다.
    display: grid;
    // [부모님: 자유너비] [관계: 75px] [이름: 80px]
    grid-template-columns: auto 75px 80px;
    justify-content: end; // 전체를 우측으로 정렬
    align-items: center;
    row-gap: 30px;
    column-gap: 14px;

    .parents {
      text-align: right;
      letter-spacing: 2px;
      white-space: nowrap;
      /* font-size는 상위 클래스를 따름 */
    }

    .sub {
      font-size: 12.5px;
      color: #888;
      text-align: left;
      letter-spacing: 1px;
      white-space: nowrap;
    }

    .name {
      width: 60px;
      display: flex;
      justify-content: space-between;

      font-weight: bold;
      font-size: 14px;
      letter-spacing: 0; // flex space-between을 쓰므로 자간은 0으로 설정해야 끝이 맞음

      span {
        display: inline-block;
        min-width: 14px; // 글자 자체가 차지하는 최소 너비
        text-align: center;
      }
    }
  }
  .names_image {
    width: 291px;
    height: 58px;
  }
  .invi_main_image {
    margin-top: 50px;
    width: 100%;
    height: auto;
  }
  .invi_main_blank {
    padding-bottom: 10px;
  }
}
</style>