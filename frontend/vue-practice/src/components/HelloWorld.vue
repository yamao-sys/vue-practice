<script setup lang="ts">
import { useDebounceFn } from '@vueuse/core';
import { computed, onBeforeMount, onBeforeUnmount, onBeforeUpdate, onMounted, onRenderTracked, onRenderTriggered, onUnmounted, onUpdated, ref, watch } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
const current = ref(new Date().toLocaleString())
const name = ref('')
const upperName = ref('')
const vBindHrefUrl = 'https://example.com'
const imgPath = ref('/vute_.svg')
const pet = ref('犬')
const agree = ref('no')
const os = ref(['Windows'])
const selectedOs = ref('Windows')
const multipleSelectedOs = ref(['Windows'])
const fileData = ref<File>()
const temparature = ref(0);
const memo = ref('')
const mails = ref([''])
const show = ref(false)
const holiday = ref('')
const book = ref({
  isbn: 'aaa',
  title: 'Javascriptの本',
  price: 100
})
const list = ref([
  '赤パジャマ',
  '青パジャマ',
  '黄パジャマ'
])
// const email = 'test@example.com'

// 算出プロパティ
// const localEmail = computed(() => {
//   return email.split('@')[0].toLowerCase()
// })
// 算出プロパティはキャッシュされる
const randomc = computed(() => {
  return Math.random()
})

// function localEmailMethod() {
//   return email.split('@')[0].toLowerCase()
// }

function onClick() {
  current.value = new Date().toLocaleString()
}
function randomm() {
  return Math.random()
}
function onErrorLoadImgPath() {
  imgPath.value = '/vite.svg'
}
function onClickArg(message: string, e: PointerEvent) {
  console.log(message)
  console.log(e)
}
function onChangeFile(e: { target: HTMLInputElement }) {
  const fl = e.target.files
  if (fl === null) {
    console.log('fdjfalkdfj')
    return
  }
  if (fl.length > 0) {
    const file = fl[0];
    fileData.value = file;
  }
}
function onChangeMemo() {
  console.log(`memoのtrim: ${memo.value}`)
}
function onClickList() {
  list.value[1] = '茶パジャマ'
}

const updateUpperName = useDebounceFn(() => {
  upperName.value = name.value.toUpperCase()
}, 2000)
// function delayFunk() {
//   setTimeout(() => {
    
//   }, 2000)
// }
watch(name, (newValue, oldValue) => {
  console.log('name newValue: ' + newValue);
  console.log('name oldValue: ' + oldValue);
  updateUpperName()
})

// // ライフサイクルフック
// // beforeCreate, createdはscript setup内に直接処理を書くようになった
// onBeforeMount(() => {
//   console.log('onBeforeMount')
// })
// onMounted(() => {
//   console.log('onMounted')
// })
// onBeforeUpdate(() => {
//   console.log('onBeforeUpdate')
// })
// onUpdated(() => {
//   console.log('onUpdated')
// })
// onBeforeUnmount(() => {
//   console.log('onBeforeUnmount')
// })
// onUnmounted(() => {
//   console.log('onUnmounted')
// })

// // renderXxx: デバッグ用途で主に使う
// onRenderTracked((e) => {
//   console.log('onRenderTracked')
//   console.log(e)
// })
// onRenderTriggered((e) => {
//   console.log('onRenderTriggered')
//   console.log(e)
// })
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Learn more about IDE Support for Vue in the
    <a
      href="https://vuejs.org/guide/scaling-up/tooling.html#ide-support"
      target="_blank"
      >Vue Docs Scaling up Guide</a
    >.
    <a v-bind:href="vBindHrefUrl">example</a>
    <a :href="vBindHrefUrl">example</a>
  </p>
  <div>
    <input type="button" value="クリック" v-bind:disabled="true" />
    <input type="button" value="クリック2" :disabled="false" @click="onClick" />
    <!-- <p>{{ localEmail }}</p>
    <p>{{ localEmailMethod() }}</p> -->
    <p>{{ current }}</p>
    <p>
      {{ randomc }}
    </p>
    <p>
      {{ randomm() }}
    </p>
    <label>名前<input type="text" v-model="name" /></label>
    <p>入力された値: {{ upperName }}</p>
    <p>
      <img :src="imgPath.value" @error="onErrorLoadImgPath" />
    </p>
    <p>
      <button @click="onClickArg('ようこそ!', $event)">クリック</button>
    </p>

    <div>
      <p>双方向データバインディング</p>
      <div>
        <p>ラジオボタン</p>

        <label for="dog">犬</label>
        <input type="radio" id="dog" value="犬" v-model="pet" />
        <label for="cat">猫</label>
        <input type="radio" id="cat" value="猫" v-model="pet" />
        <label for="other">その他</label>
        <input type="radio" id="other" value="その他" v-model="pet" />
        <p>ペット: {{ pet }}</p>
      </div>
      <div>
        <p>チェックボックス(単一)</p>

        <label for="agree">同意する</label>
        <input type="checkbox" id="agree" v-model="agree" true-value="yes" false-value="no" />
        <p>回答: {{ agree }}</p>
      </div>
      <div>
        <p>チェックボックス(複数)</p>

        <label for="windows">Windows</label>
        <input type="checkbox" id="windows" value="Windows" v-model="os" />
        <label for="mac">Mac</label>
        <input type="checkbox" id="mac" value="Mac" v-model="os" />
        <label for="linux">Linux</label>
        <input type="checkbox" id="linux" value="Linux" v-model="os" />
        <p>OS: {{ os }}</p>
      </div>
      <div>
        <p>セレクトボックス(単一)</p>

        <label for="os">お使いのOSは？</label>
        <select id="os" v-model="selectedOs">
          <option value="">OSを選択してください</option>
          <option>Windows</option>
          <option>Mac</option>
          <option>Linux</option>
        </select>
        <p>回答: {{ selectedOs }}</p>
      </div>
      <div>
        <p>セレクトボックス(複数)</p>

        <label for="multiple-os">お使いのOSは？(複数選択可)</label>
        <select id="multiple-os" v-model="multipleSelectedOs" multiple size="3">
          <option>Windows</option>
          <option>Mac</option>
          <option>Linux</option>
        </select>
        <p>回答: {{ multipleSelectedOs }}</p>
      </div>
      <div>
        <p>ファイル入力</p>

        <label for="upload-file">ファイル入力</label>
        <input type="file" id="upload-file" @change="onChangeFile" />
        <p>データ: {{ fileData }}</p>
      </div>
      <div>
        <label for="temparature">サウナの温度: </label>
        <input type="text" id="temparature" v-model.number="temparature" />
      </div>
      <div>
        <label for="memo">メモ: </label>
        <input type="text" id="memo" v-model.trim="memo" @change="onChangeMemo" />
      </div>
      <div>
        <label for="mail">メールアドレス: </label>
        <textarea id="mail" :value="mails.join(';')" @input="mails=$event.target.value.split(';')" />
        <ul>
          <li :key="mail" v-for="mail in mails">{{ mail }}</li>
        </ul>
        <ul>
          <li :key="i" v-for="(mail, i) in mails">{{ mail }}</li>
        </ul>
      </div>
      <div>
        <label for="show">表示/非表示</label>
        <input type="checkbox" id="show" v-model="show" />
        v-ifはtrueになって初めて要素自体が出力される。v-showはOFFの時はdisplay: noneになっている
        パフォーマンスの観点から、一度表示されたら滅多に非表示にならなければ、v-if 頻繁に変わるものはv-show
        <div v-if="show">
          表示中！
        </div>
        <div v-else>現在、非表示中です</div>
        <div v-show="show">
          v-showにより表示中！
        </div>
      </div>
      <div>
        <label for="holiday">祝日: </label>
        <select id="holiday" v-model="holiday">
          <option value="">祝日を選択してください。</option>
          <option value="new">元日</option>
          <option value="child">子どもの日</option>
          <option value="culture">文化の日</option>
          <option value="labor">勤労感謝の日</option>
        </select>
        <div v-if="holiday === 'new'">1月1日。年の初めを祝う</div>
        <div v-else-if="holiday === 'child'">5月5日</div>
        <div v-else-if="holiday === 'culture'">11月3日</div>
        <div v-else-if="holiday === 'labor'">11月23日</div>
        <div v-else>未選択</div>
      </div>
      <div>
        <p>オブジェクトのプロパティを順に処理</p>
        <ul>          
          <li v-for="(value, key) in book" :key="key">
            {{ key }}: {{ value }}
          </li>
        </ul>
      </div>
      <!-- <div>
        <p>templateを使用して不要な要素の出力を防ぐ</p>
        <template v-for="(value, key, i) in book">
          <template :key="key"><p>{{ i }}: {{ key }}: {{ value }}</p></template>
        </template>
      </div> -->
      <div>
        <label for="pajama">パジャマ</label>
        <input type="button" value="変更" @click="onClickList"/>
        <ul>
          <li v-for="item in list" :key="item">{{ item }}</li>
        </ul>
      </div>
      <div :style="{ backgroundColor: 'red', fontSize: '1.5rem' }">Hello!</div>
      <div v-cloak>{{ count }}</div>
    </div>
  </div>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
[v-cloak] {
  display: none
}
</style>
