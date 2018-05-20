<template>
<!--ログインしてる時としてない時で表示を変える-->
<!--ログインしてる時Home.vueログインしてない時Editor.vue-->
<!-- コンポーネントの読み込み -->
<div id ="app">
<Home v-if="!isLogin"></Home>
<Editor v-if="isLogin" :user="userData"></Editor>
</div>
</template>
<!--vueファイルの読み込み-->
<script>
import Home from './components/Home.vue';
import Editor from './components/Editor.vue';

//trueでエディタ表示
export default {
  name:'app',
  data(){
    return {
      isLogin: false,
      userData: null,
    }
  },
//ログイン状態ならuserにユーザー情報が格納される
//userが存在したらログインしているので、true/false分岐
  created: function() {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);
      if (user) {     
        this.isLogin = true;
        this.userData = user;
      } else {
        this.isLogin = false;
        this.userData = null;
      };
    });
  },
// tag名：読み込んだvueファイル
  components:{
    'Home':Home,
    'Editor':Editor,
  },
}
</script>