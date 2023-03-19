<template>
  <div class="card">
    <h1>GOST</h1>
    <input type="text" v-model="str" />
    <p>
      Result: {{ encryptedStr }}
    </p>
  </div>
</template>

<script>
import { Buffer } from 'buffer';
import { gostCrypto, gostEngine } from 'node-gost-crypto';

export default {
  name: 'Gost',
  data() {
    return {
      str: 'Hello World!'
    };
  },
  computed: {
    encryptedStr() {
      const buffer = Buffer.from(this.str)
      const digest = gostEngine.getGostDigest({ name: 'GOST R 34.11', length: 256, version: 1994 })
      return Buffer.from(digest.digest(buffer)).toString('hex')
    }
  }
};

</script>