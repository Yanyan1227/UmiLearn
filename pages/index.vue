<!--
 * @Author: uyinyan yinyan2323@qq.com
 * @Date: 2024-08-27 14:37:59
 * @LastEditors: uyinyan yinyan2323@qq.com
 * @LastEditTime: 2024-08-27 19:15:14
 * @FilePath: /umi/umiNuxt/pages/index.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <div>
    Hellow World
    {{ testData }}
    {{ testData1 }}
    <button>
      <NuxtLink to="/test">Home page</NuxtLink>
      跳转
    </button>

    <NuxtLogo>

    </NuxtLogo>
  </div>

</template>

<script>
export default {
  data() {
    return {
      testData: [],
      testData1: []
    }
  },
  async asyncData() {
    let data = []
    data = await fetch(
      'https://jsonplaceholder.typicode.com/todos/1'
    ).then(res => res.json()).then(json => data = json)
    console.log(data, 'datadata1111')
    // 1. asyncData fetch来回切换路由，process.server和process.client的执行结果
    // 2. asyncData fetch强刷页面，process.server和process.client的执行结果
    console.log(process.server, 'asyncData-server')
    console.log(process.client, 'asyncData-client')
    // await new Promise(resolve => {
    //   setTimeout(() => {
    //     data = [12]
    //     resolve()
    //   }, 1000 * 3600)
    // })

    // 一个个执行会阻塞
    return {
      testData: data
    }
  },
  // 正确
  async fetch() {
    let testData1 = null
    await fetch(
      'https://jsonplaceholder.typicode.com/todos/1'
    ).then(res => res.json()).then(json => testData1 = json)
    testData1.qaz = '>>>'
    this.testData1 = testData1
    console.log(this, 'vue')
  },
  // 错误典范
  async fetch() {
    let testData = await fetch(
      'https://jsonplaceholder.typicode.com/todos/1'
    ).then(res => res.json())
    testData = this.testData
    return {
      testData
    }
  }
}
// 3. asyncData fetch可以在什么页面层级去用？页面和组件去是试试看
// 4. 同1和2, 也看看fetch的打印结果
// 5. asyncData和fetch的区别
// 6. vue2去补
//   async fetch() {
//     console.log(process.server, 'fetch-server')
//     console.log(process.client, 'fetch-client')
//     await new Promise(resolve => {
//       setTimeout(() => {
//         data = [12]
//         resolve()
//       }, 1000 * 3600)
//     })
//   }

// 并行
</script>
