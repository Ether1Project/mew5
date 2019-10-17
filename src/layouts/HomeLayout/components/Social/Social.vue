<template>
  <div class="social">
    <div class="wrap">
      <div class="page-container">
        <div class="flex-col-vertical-center content">
          <div class="title">
            <h2>{{ $t('home.socialTitle') }}</h2>
            <h5>{{ $t('home.socialSubheading') }}</h5>
          </div>
          <div class="icons">
            <a
              v-for="(link, index) in links"
              :href="link.to"
              :key="link.name + index"
              :aria-label="link.name"
              target="_blank"
              rel="noopener noreferrer"
            >
              <div :class="link.name">
                <img :src="link.img" alt />
                <p>{{ link.name | capitalize }}</p>
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import github from '@/assets/images/icons/github.png';
import medium from '@/assets/images/icons/medium.png';
import twitter from '@/assets/images/icons/twitter.jpg';

export default {
  data() {
    return {
      links: [
        {
          img: twitter,
          to: 'https://twitter.com/Ether1Official',
          name: 'Twitter'
        },
        {
          img: medium,
          to: 'https://medium.com/Ether1Official',
          name: 'Medium'
        },
        {
          img: github,
          to: 'https://github.com/Ether1Project',
          name: 'github'
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
@import 'Social.scss';
</style>
