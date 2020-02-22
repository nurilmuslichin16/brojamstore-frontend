<template>
  <div class="home">
    <HeaderBrojam />
    <HeroBrojam />
    <BannerBrojam />
    <InstaBrojam />
    <PartnerBrojam />
    <FooterBrojam />
  </div>
</template>

<script>
import HeaderBrojam from '@/components/HeaderBrojam.vue'
import HeroBrojam from '@/components/HeroBrojam.vue'
import BannerBrojam from '@/components/BannerBrojam.vue'
import InstaBrojam from '@/components/InstaBrojam.vue'
import PartnerBrojam from '@/components/PartnerBrojam.vue'
import FooterBrojam from '@/components/FooterBrojam.vue'

export default {
  name: 'Home',
  components: {
    HeaderBrojam,
    HeroBrojam,
    BannerBrojam,
    InstaBrojam,
    PartnerBrojam,
    FooterBrojam
  }
}
</script>