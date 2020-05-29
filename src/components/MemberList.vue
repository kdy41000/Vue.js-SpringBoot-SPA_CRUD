<template>
    <table border="1">
        <thead v-if="memberlist.length > 0">
            <tr>
            <th>번호</th>
            <th class="nameth">이름</th>
            <th class="titleth">제목</th>
            <th>작성일</th>
            <th>수정</th>
            <th>삭제</th>
            </tr>
        </thead>    
        <tbody id="memberlist">
            <tr v-for="m in memberlist" :key="m.no">
                <td>{{m.no}}</td>
                <td class="tdcenter">{{m.name}}</td>
                <td class="tdcenter">{{m.title}}</td>
                <td>{{m.wrtdate}}</td>
                <td><button small color="primary" @click="updateform(m.no)">수정</button></td>
                <td><button @click="deletemember(m.no)">삭제</button></td>
            </tr>    
        </tbody>    
    </table>    
</template>
<script>
import axios from 'axios';
import eventBus from '../EventBus.js';

export default {
   props : ['memberlist'],
   methods : {
       deletemember : function(paramno) {

           axios({
               method : 'POST',
               url : '/delete',
               params : { no : paramno }
           })
           .then((response) => {
               if(response.data == true){
                alert("삭제완료");
                eventBus.$emit("complete");
               }
           })
           .catch(() => {
               console.log('ERROR!!!');
           })
       },
       updateform : function(paramno) {
           eventBus.$emit("updateform",paramno);
       }
   }
}
</script>

<style scoped>
.nameth{ width:200px; }
.titleth{ width:300px; }
.tdcenter{ text-align:center; }
</style>