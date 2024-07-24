<template>
  <div>
    <qrcode-vue :value="qrCodeValue" :size="150" id="qrcode"></qrcode-vue>
  </div>
</template>

<script>
import QRCodeVue from 'qrcode.vue';
import { EventBus } from '@/assets/scripts/eventBus';

export default {
  props: ['genInfo'],
  components: {
    'qrcode-vue': QRCodeVue
  },
  data() {
    return {
      qrCodeValue: ''
    };
  },
  created() {
    EventBus.$on('update-qr-code', this.updateQRCode);
  },
  beforeDestroy() {
    EventBus.$off('update-qr-code', this.updateQRCode);
  },
  methods: {
    updateQRCode(vCardData) {
      this.qrCodeValue = vCardData;
    }
  }
};
</script>

<style scoped>
form {
  margin-bottom: 20px;
}
</style>
