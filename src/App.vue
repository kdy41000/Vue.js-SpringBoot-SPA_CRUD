<template>
  <div id="app">
    <button @click="listCall">멤버목록</button>
    <button @click="changeMenu('insert-page')">등록</button>
    <member-list :memberlist="memberlist" ></member-list>

    <div class="container">
      <component v-bind:is="currentView" :contents="contents"></component>
    </div>
  </div>
</template>

<script>
import MemberList from './components/MemberList.vue'
import InsertPage from './components/InsertPage.vue'
import UpdatePage from './components/UpdatePage.vue'
import axios from 'axios';
import eventBus from './EventBus.js';

export default {
  name: 'App',
  components: { MemberList, InsertPage, UpdatePage },
  data : function() {
    return { 
        currentView : '',
        memberlist : '',
        contents : ''
      }
  },
  mounted : function() {
    eventBus.$on("complete", () => {   // 이벤트버스 응답이 오면 전체조회
       this.listCall();
    });
    eventBus.$on("updateform", (paramno) => {   // 업데이트 전 select
     // alert(paramno);
      axios({
        method : 'POST',
        url : '/updatebeforeselect',
        params : { no : paramno }
      })
      .then((response) => {
        this.contents = response.data;
        this.changeMenu('update-page');
      })
      .catch(() => {
        console.log('ERROR!!!');
      })
    })
  },
  methods : {
    listCall : function(){   //전체 리스트 호출
      this.currentView = '';
      axios({
        method : 'GET',
        url : '/list'
      })
      .then((response) => {
         console.log(response);
         this.memberlist = response.data;
      })
      .catch(() => {
        console.log('ERROR!!');
      })
    },
    changeMenu(curview) {   //동적컴포넌트
      this.memberlist = '';
      this.currentView = curview;
    }
  }
}
</script>

<style>
</style>
