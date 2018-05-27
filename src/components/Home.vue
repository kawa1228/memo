<template>
<div id ="home">
    <h1>{{ msg }}</h1>　<!--@clickはHTMLのonClickみたいなもの-->
    <button @click="googleLogin">Google アカウントでログイン</button>
</div>
</template>

<script>
export default {
    name:'home',
    data(){
        return{
            msg:'Welcome to Memo'
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