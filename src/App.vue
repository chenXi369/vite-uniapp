<script setup>
// #ifdef WEB
import { updateShades } from '$unocss-preset-shades'
// #endif
import cloudbase from '@cloudbase/js-sdk'

onLaunch(() => {
  console.log('App Launch')
  const app = cloudbase.init({
    env: 'cloud1-1gfbbvv053a92dde',
    accessKey: 'eyJhbGciOiJSUzI1NiIsImtpZCI6IjlkMWRjMzFlLWI0ZDAtNDQ4Yi1hNzZmLWIwY2M2M2Q4MTQ5OCJ9.eyJpc3MiOiJodHRwczovL2Nsb3VkMS0xZ2ZiYnZ2MDUzYTkyZGRlLmFwLXNoYW5naGFpLnRjYi1hcGkudGVuY2VudGNsb3VkYXBpLmNvbSIsInN1YiI6ImFub24iLCJhdWQiOiJjbG91ZDEtMWdmYmJ2djA1M2E5MmRkZSIsImV4cCI6NDA5NzU1MTYzNiwiaWF0IjoxNzYyMzMyNDM2LCJub25jZSI6ImF2Rm1MU3dxU0R5ZWNhUjNvSnhCREEiLCJhdF9oYXNoIjoiYXZGbUxTd3FTRHllY2FSM29KeEJEQSIsIm5hbWUiOiJBbm9ueW1vdXMiLCJzY29wZSI6ImFub255bW91cyIsInByb2plY3RfaWQiOiJjbG91ZDEtMWdmYmJ2djA1M2E5MmRkZSIsInVzZXJfdHlwZSI6IiJ9.Twoj8CLmIlBVI-uMElGxXSKti-c-dknqasza8GxeXNMSNjEQsZkEZcgdWaJNz4nVjpL7CRLwbe7P47PurZKxjBS4Mwpe8WTbSmnz8K5PuqwyU_d_bcxmrgGeIwq-av0kjUiTdZkCohtuaCJzbksTanDP3DZfxwbbTRsA0jkWJT2frJYYPN31CAI1JtW7AWBFj13UfqS2jMNOGd-OwYchyyf35bUqtXuvTkeyC5vxWckmzBol6sWMyQZbq_YssJ09nRWdUjbRlPfletqGbN76Dp8UOV7eu59zFrSjcuzNeg9l965oxrmRYqhlr4pl7mpx4oiNAQXhGTs8ueGodgIgng', // 填入生成的 Publishable Key
  })

  // 初始化SDK实例部分代码如上
  app
    .getTempFileURL({
      fileList: [
        'cloud://cloud1-1gfbbvv053a92dde.636c-cloud1-1gfbbvv053a92dde-1327228305/custom-font-family/AlimamaFangYuanTiVF-Thin.ttf',
      ],
    })
    .then((res) => {
      res.fileList.forEach((el) => {
        if (el.code === 'SUCCESS') {
          uni.loadFontFace({
            family: 'Bitstream Vera Serif Bold', // 定义的字体名称
            source: `url(${el.tempFileURL})`, // 服务器字体地址
            global: true, // 全局字体，
            success: (res) => {
              console.log('字体加载成功', res)
            },
            fail: (err) => {
              console.error('字体加载失败', err)
            },
          })
        }
      })
    })
})
onShow(() => {
  console.log('App Show')
})
onHide(() => {
  console.log('App Hide')
})

const appStore = useAppStore()

// #ifdef WEB
watchEffect(() => {
  updateShades(appStore.primaryColor)
})
// #endif
</script>

<style lang="scss">
// #ifndef APP-NVUE
@import '@unocss-applet/reset/uni-app/button-after.css';
@import '@unocss-applet/reset/uni-app/tailwind-compat.css';
// #endif
@import './styles/css/index.css';

.font-custom {
  font-family: 'Bitstream Vera Serif Bold';
}
</style>
