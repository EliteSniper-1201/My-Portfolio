<template>
  <div ref="Contact" class="contact">
    <AppCircleBg :state="isCircleBgState" :modifier="'index-contact'" />
    <div class="contact-bg">
      <div class="contact-inner">
        <div class="l-container">
          <h2 class="contact-title">
            <span class="contact-title-read-area">
              <AppReadTitle :state="isTextSegmentState" :text="['・', 'SAY HI']" :modifier="'section'" />
            </span>
            <span class="pc-only">
              <span class="contact-title-wrapper contact-title-wrapper-01">
                <AppTextAnimation :state="isTextSegmentState" :rotate="$BASEROTATE.right" :text="'I AM FRONTEND DEVELOPER'" :sp-animation="false" />
              </span>
              <span class="contact-title-wrapper contact-title-wrapper-02">
                <AppTextAnimation :state="isTextSegmentState" :start="0.12" :rotate="$BASEROTATE.left" :text="'FOCUSED ON CREATING THINGS'" :sp-animation="false" />
              </span>
              <span class="contact-title-wrapper contact-title-wrapper-03">
                <AppTextAnimation :state="isTextSegmentState" :start="0.24" :rotate="$BASEROTATE.right" :text="'WITH INTERACTION & ANIMATION'" :sp-animation="false" />
              </span>
              <span class="contact-title-wrapper contact-title-wrapper-04">
                <AppTextAnimation :state="isTextSegmentState" :start="0.36" :rotate="$BASEROTATE.left" :text="'AS MY MAIN FOCUS.'" :sp-animation="false" />
              </span>
            </span>
            <span class="sp-only">
              <span class="contact-title-wrapper contact-title-wrapper-01-sp"> I AM FRONTEND </span>
              <span class="contact-title-wrapper contact-title-wrapper-02-sp"> DEVELOPER </span>
              <span class="contact-title-wrapper contact-title-wrapper-03-sp"> FOCUSED ON </span>
              <span class="contact-title-wrapper contact-title-wrapper-04-sp"> CREATING THINGS </span>
              <span class="contact-title-wrapper contact-title-wrapper-05-sp"> WITH INTERACTION </span>
              <span class="contact-title-wrapper contact-title-wrapper-06-sp"> & ANIMATION </span>
              <span class="contact-title-wrapper contact-title-wrapper-07-sp"> AS MY MAINN FOCUS. </span>
            </span>
          </h2>
          <div class="contact-info-area">
            <div class="contact-info-index-area">
              <span class="contact-info-index">
                <AppReadTitle :state="isTextSegmentState" :start="0.48" :text="['・', 'INDEX']" :modifier="'contact-section'" />
              </span>
              <ul class="contact-info-list">
                <li v-for="(data, index) in projectData" :key="data.id" class="contact-info-item js-click-target">
                  <AppPageTransitionImage :url="`works/${data.id}`" :index="index">
                    <AppTextAnimation :state="isTextSegmentState" :start="0.48 + index * 0.12" :rotate="$BASEROTATE.right" :text="data.title.full" />
                  </AppPageTransitionImage>
                </li>
                <li class="contact-info-item js-click-target">
                  <AppPageTransitionBg :url="`archive`" color="#000000">
                    <AppTextAnimation :state="isTextSegmentState" :start="0.48 + projectData.length * 0.12" :rotate="$BASEROTATE.right" :text="'ARCHIVE'" />
                  </AppPageTransitionBg>
                </li>
              </ul>
            </div>
            <div class="contact-info-name-area">
              <span class="pc-only">
                <span class="contact-name">
                  <AppTextAnimation :state="isTextSegmentState" :start="0.48" :rotate="$BASEROTATE.right" :text="'JURI MIYAZAWA'" :sp-animation="false" />
                </span>
              </span>
              <span class="sp-only">
                <span class="contact-name"> JURI<br />MIYAZAWA </span>
              </span>
            </div>
          </div>
          <div class="contact-card-item-01">
            <AppCard
              :component-name="'contact'"
              :name="['・', 'DESIGNED BY', '(KENTO ISHIDUKA)']"
              :info="[
                {
                  link: contactData[1].list01.link,
                  text: contactData[1].list01.text,
                },
                {
                  link: contactData[1].list02.link,
                  text: contactData[1].list02.text,
                },
                {
                  link: contactData[1].list03.link,
                  text: contactData[1].list03.text,
                },
              ]"
              :title="{
                text: contactData[1].mainTitle.title,
                link: '',
                subtext: '',
              }"
              :rotate="-10"
              :xspeed="-0.08"
              :yspeed="0.2"
            />
          </div>
          <div class="contact-card-item-02">
            <AppCard
              :component-name="'contact'"
              :name="['・', 'CODED BY', '(JURI MIYAZAWA)']"
              :info="[
                {
                  link: contactData[0].list01.link,
                  text: contactData[0].list01.text,
                },
                {
                  link: contactData[0].list02.link,
                  text: contactData[0].list02.text,
                },
                {
                  link: contactData[0].list03.link,
                  text: contactData[0].list03.text,
                },
              ]"
              :title="{
                text: contactData[0].mainTitle.title,
                link: contactData[0].mainTitle.link,
                subtext: contactData[0].mainTitle.subtitle,
              }"
              :rotate="8"
              :xspeed="0.051"
              :yspeed="0.1"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    projectData: {
      type: Array,
      required: true,
    },
    contactData: {
      type: Array,
      required: true,
    },
  },

  data: () => {
    return {
      isTextSegmentState: '',
      isCircleBgState: '',
    }
  },

  mounted() {
    /* text-animation */
    this.observe = this.$refs.Contact
    this.iObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            this.isTextSegmentState = 'center'
            this.isCircleBgState = 'extend'
            this.iObserver.unobserve(this.observe)
          }
        })
      },
      { rootMargin: '0%' }
    )
    this.iObserver.observe(this.observe)
  },

  beforeDestroy() {
    this.iObserver.unobserve(this.observe)
    this.iObserver = null
  },
}
</script>

<style scoped lang="scss">
.contact {
  position: relative;
}

.contact-bg {
  padding: 450px 0 0 0;

  @include tab() {
    padding: 335px 0 0 0;
  }

  @include sp() {
    padding: 225px 0 80px 0;
  }
}

.contact-title {
  position: relative;
  margin: 0 0 140px 0;
  color: $darkPink;
  font-size: vw(180);
  font-family: $sixcaps;

  @include tab() {
    font-size: vw(170);
  }

  @include tab-vertical() {
    font-size: vw(150);
  }

  @include sp() {
    margin: 0 0 58px 0;
    font-size: vw_sp(180);
  }
}

.contact-title-read-area {
  position: absolute;
  top: 8px;
  left: 2px;
  color: $white;

  @include sp() {
    top: 2px;
    left: 0;
  }
}

.contact-title-wrapper {
  display: block;

  @include sp() {
    white-space: nowrap;
  }
}

.contact-title-wrapper-01 {
  padding: 0 0 0 290px;

  @include tab {
    padding: 0 0 0 vw(290);
  }
}

.contact-title-wrapper-02 {
  padding: 0 0 0 33px;
}

.contact-title-wrapper-04 {
  padding: 0 0 0 40px;
}

.contact-title-wrapper-01-sp {
  margin: 0 0 0 48px;
}

.contact-info-area {
  display: flex;

  @include sp() {
    justify-content: space-between;
  }
}

.contact-info-index-area {
  margin: vw(32) 40px 0 0;

  @include tab-vertical() {
    margin: vw(16) 40px 0 0;
  }

  @include sp() {
    margin: 10px 40px 0 0;
  }
}

.contact-info-index {
  display: block;
  margin: 0 0 56px 0;

  @include tab-vertical() {
    margin: 0 0 20px 0;
  }

  @include sp() {
    margin: 0 0 59px 0;
  }
}

.contact-info-list {
  font-size: 12px;

  @include sp() {
    font-size: 10px;
  }
}

.contact-info-item {
  @include sp() {
    display: block;
    margin: 0 0 2px 0;
  }
}

.contact-info-name-area {
  position: relative;
}

.contact-name {
  margin: -26px 0 0 0;
  color: $darkPink;
  font-size: vw(400);
  font-family: $sixcaps;
  letter-spacing: -0.02em;

  @include tab() {
    font-size: vw(380);
  }

  @include tab-vertical() {
    font-size: vw(320);
  }

  @include sp() {
    font-size: vw_sp(400);
    white-space: nowrap;
  }
}

.contact-card-item-01 {
  position: absolute;
  top: 69.5%;
  left: 24%;
  transform: rotate(-10deg);
  width: 0;
  height: 0;

  @include sp() {
    top: 48%;
    left: 38%;
  }
}

.contact-card-item-02 {
  position: absolute;
  top: 60%;
  right: 38%;
  transform: rotate(10deg);
  width: 0;
  height: 0;

  @include sp() {
    top: 46%;
    right: 50%;
  }
}
</style>
