<!--
 * @Author: uyinyan yinyan2323@qq.com
 * @Date: 2024-08-27 14:37:59
 * @LastEditors: uyinyan yinyan2323@qq.com
 * @LastEditTime: 2024-08-27 18:54:23
 * @FilePath: /umi/umiNuxt/components/NuxtLogo.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <div>
    qqq
    {{ testData }}
  </div>
</template>
<script>

export default {
  data() {
    return {
      testData: []
    }
  },
  async fetch() {
    let data = [7777777]
    console.log(process.server, 'fetch-server')
    console.log(process.client, 'fetch-client')
    await new Promise(resolve => {
      setTimeout(() => {
        this.testData = data
        resolve()
      }, 1000)
    })
  }
}
</script>
