<template>
<div id ="home">
    <title>{{ titile }}</title>
    <h1>{{ msg }}</h1>　<!--@clickはHTMLのonClickみたいなもの-->
    <h2>オンラインで簡単メモ作成</h2>
    <button @click="googleLogin">Google アカウントでログイン</button>
    <ul>
        <li>
            <a href="#">利用規約</a>
        </li>
        <li>
            <a href="#">プライバシーポリシー</a>
        </li>
    </ul>
</div>
</template>

<script>
export default {
    name:'home',
    data(){
        return{
            msg:'Welcome to Memo',
            title:'めも'
        }
    },
    //googleLoginという関数の内容を記載
    methods:{
        googleLogin:function(){
            firebase.auth().signInWithRedirect(new firebase.auth.GoogleAuthProvider());
        }
    }
}
</script>