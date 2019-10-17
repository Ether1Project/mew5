<template>
  <div class="footer">
    <!-- Modal -->
    <feedback-modal />
    <div class="wrap">
      <div class="page-container">
        <div class="grid-col-1-1-1-2 footer-contents">
          <div
            v-for="(item, index) in footerContent"
            :ref="item.class"
            :class="item.class"
            :key="item.title + index"
          >
            <div class="content-title" @click="toggler(item.class)">
              <h3 class="lite">{{ item.title }}</h3>
              <p class="open" @click="openContent(item.class)">
                <i class="fa fa-plus" aria-hidden="true" />
              </p>
              <p class="close" @click="closeContent(item.class)">
                <i class="fa fa-minus" aria-hidden="true" />
              </p>
            </div>
            <div class="content-links">
              <div class="content-links-animation-block">
                <div
                  v-for="(content, index) in item.contents"
                  :key="content.text + index"
                  class="content"
                >
                  <div v-if="content.text === $t('common.customerSupport')">
                    <customer-support :no-icon="true" />
                  </div>
                  <router-link
                    v-else-if="content.to !== undefined"
                    :to="content.to"
                  >
                    <p>{{ content.text }}</p>
                  </router-link>
                </div>
              </div>
            </div>
          </div>
          <div class="donate-us">
            <div class="content-title">
              <h3 class="lite">
                {{ $t('footer.donate') }}
              </h3>
            </div>
            <div class="links">
              <p>{{ $t('footer.welcomeDes') }}</p>
              <p class="crypto-link">
                &nbsp;Ethereum / ETHO
                0xB69B9216B5089Dc3881A4E38f691e9B6943DFA11
              </p>

              <a
                href="https://blockchain.info/address/1ucuBe2hAhWWj5bVcDKVBsYaT37wdcd1n"
                target="_blank"
                rel="noopener noreferrer"
              >
                <p
                  class="crypto-link no-padding"
                  data-btc="1ucuBe2hAhWWj5bVcDKVBsYaT37wdcd1n"
                >
                  <img src="~@/assets/images/icons/btc.svg" alt /> &nbsp;Bitcoin
                  Donation
                </p>
              </a>
            </div>
          </div>
        </div>
        <div class="flex-space-between foot-note">
          <div class="links">
            <div v-for="(link, index) in lowerLinks" :key="link.title + index">
              <router-link v-if="link.hasOwnProperty('to')" :to="link.to">
                <span>{{ link.title }}</span>
              </router-link>
              <a
                v-else
                :href="link.href"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span>{{ link.title }}</span>
              </a>
            </div>
          </div>
          <div class="copyright">
            <p>
              {{ $t('footer.copyright') }}
            </p>
          </div>
          <div class="social">
            <a
              v-for="link in links"
              :href="link.to"
              :key="link.class"
              :aria-label="link.to"
              rel="noopener noreferrer"
              target="_blank"
            >
              <i :class="'fa ' + link.class" />
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import FeedbackModal from '@/components/FeedbackModal';
import CustomerSupport from '@/components/CustomerSupport';
import affiliates from './affiliates.js';
const version = VERSION;

export default {
  components: {
    'feedback-modal': FeedbackModal,
    'customer-support': CustomerSupport
  },
  data() {
    return {
      version: version,
      lowerLinks: [
        {
          title: this.$t('footer.feedback'),
          href: 'mailto:ethan@ether1.org'
        },
        {
          title: `v${version}`,
          href: `https://github.com/MyEtherWallet/MyEtherWallet/releases/tag/v${version}`
        }
      ],
      footerContent: [
        {
          class: 'e1',
          title: this.$t('footer.discover'),
          contents: [
            {
              text: this.$t('footer.units'),
              to: '/convert-units'
            }
          ]
        },
        {
          class: 'e2',
          title: this.$t('footer.affiliates'),
          contents: affiliates
        },
        {
          class: 'e3',
          title: this.$t('footer.mew'),
          contents: [
            {
              text: this.$t('common.customerSupport'),
              href: 'mailto:ethan@ether1.org'
            }
          ]
        }
      ],
      links: [
        {
          to: 'https://twitter.com/Ether1Official',
          class: 'fa-twitter'
        },
        {
          to: 'https://github.com/Ether1Project',
          class: 'fa-github'
        },
        {
          to: 'https://medium.com/@Ether1Official',
          class: 'fa-medium'
        }
      ]
    };
  },
  computed: {
    ...mapState(['ethDonationAddress'])
  },
  methods: {
    openFeedbackModal() {
      this.$children[0].$refs.feedback.show();
    },
    openContent(element) {
      const openButton = document.querySelector('.' + element + ' .open');
      const closeButton = document.querySelector('.' + element + ' .close');
      const content = document.querySelector('.' + element + ' .content-links');
      openButton.style.display = 'none';
      closeButton.style.display = 'block';
      content.classList.remove('mobile-hide');
    },
    closeContent(element) {
      const openButton = document.querySelector('.' + element + ' .open');
      const closeButton = document.querySelector('.' + element + ' .close');
      const content = document.querySelector('.' + element + ' .content-links');
      openButton.style.display = 'block';
      closeButton.style.display = 'none';
      content.classList.add('mobile-hide');
    },
    toggler(ref) {
      const el = this.$refs[ref][0];
      el.classList.toggle('content-open');
    }
  }
};
</script>

<style lang="scss" scoped>
@import 'FooterContainer-desktop.scss';
@import 'FooterContainer-tablet.scss';
@import 'FooterContainer-mobile.scss';
</style>
