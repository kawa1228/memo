<template>
<div class="editor">
    <div class="editorContainer">
        <h1 class="EditorTitle">Online Memo Editor</h1>
        <button class="logout" @click="logout">　Logout <i class="fas fa-sign-out-alt"></i></button>
        <span>{{ user.displayName }}</span>
    </div>

    <div class="main">
        <div class="memoListWrapper">
            <div class="buttonList">
                <button class="addMemoBtn" @click="addMemo"><i class="fas fa-plus"></i></button>
                <button class="deleateMemoBtn" v-if="memos.length>1" @click="deleteMemo"><i class="fas fa-trash-alt"></i></button>
                <button class="saveMemosBtn" @click="saveMemos"><i class="far fa-save"></i></button>
            </div>
                <div class="memoList"  v-for="(memo, index) in memos" @click="selectMemo(index)" v-bind:data-selected="index == selectedIndex">
                    <p class="memoTitle">{{ displayTitle(memo.markdown)}}</p>
                </div>

        </div>
        <textarea class="markdown" v-model="memos[selectedIndex].markdown"></textarea>
        <div class="previewArea"> <p class="area">Preview Area </p>
           <div class="preview" v-html="preview()"></div>
        </div>
    </div>
</div>
</template>

<script>
import marked from 'marked';

export default {
    name: 'editor',
    props: ['user'],
    data() {
        return{
            memos:[{
            markdown: '' 
            }],
            selectedIndex: 0
        }
    },
    created:function(){
        firebase
        .database()
        .ref('memos/'+this.user.uid)
        .once('value')
        .then(result=>{
            if(result.val()){
                this.memos=result.val();
            }
        })
    },
    methods: {
        logout:function(){
            firebase.auth().signOut();
        },
        addMemo:function(){
            this.memos.push({
                markdown:'無題のメモ',
            })
        },
        selectMemo:function(index){
          this.selectedIndex = index;
        },
        preview:function(){
            return marked(this.memos[this.selectedIndex].markdown);
        },
        displayTitle:function(text){
            return text.split(/\n/)[0];
        },
        deleteMemo:function(){
            this.memos.splice(this.selectedIndex,1);
            if(this.selectedIndex>0){
                this.selectedIndex--;
            }
        },
        saveMemos:function(){
            firebase
            .database()
            .ref('memos/'+this.user.uid)
            .set(this.memos);
        },
    }
}
</script>