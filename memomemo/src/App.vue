<template>
<!--ログインしてる時としてない時で表示を変える-->
<!--ログインしてる時Home.vueログインしてない時Editor.vue-->
<!-- コンポーネントの読み込み -->
<div id ="app">
<Home v-if="!isLogin"></Home>
<Editor v-if="isLogin"></Editor>
</div>
</template>
<!--vueファイルの読み込み-->
<script>
import Home from './components/Home.vue';
import Editor from './components/Editor.vue';


export default {
  name:'app',
  data(){
    return{
    isLogin:false
  }
},
// tag名：読み込んだvueファイル
components:{
  'Home':Home,
  'Editor':Editor,
},
}
</script>