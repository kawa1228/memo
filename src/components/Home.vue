<template>
<div id ="home">
    <div class="container">
    <h1 class="title">{{ msg }}</h1>　<!--@clickはHTMLのonClickみたいなもの-->
    <h2>オンラインで簡単メモ作成</h2>
    <div class="login"><button @click="googleLogin"><i class="fab fa-google googleIcon"></i>　Google アカウントでログイン</button></div>
    <div class="editorImage"><img alt="editorImage" src="../assets/Editor.png"></div>
        <ul>
            <li class="news"><p class="date">　　2018/06/03　　</p><p class="updata">サイト公開しました</p></li>
        </ul>
    <div class="footer">
    <ul>
        <li>
            <a href="#">利用規約</a>
        </li>
        <li>
            <a href="#">プライバシーポリシー</a>
        </li>
    </ul>
    </div>
    </div>
</div>
</template>

<script>
export default {
    name:'home',
    data(){
        return{
            msg:'Online Memo Editor',
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