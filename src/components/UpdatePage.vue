<template>
    <div>
        번호 : <input type="text" disabled v-model="no" /><br/>
        이름 : <input type="text" v-model.trim="name" value="contents.name" /><br/>
        제목 : <input type="text" v-model.trim="title" value="contents.title" /><br/>
        날짜 : <input type="text" disabled v-model="wrtdate" /><br/>
        <button @click="updatemember">수정</button>
    </div>
</template>
<script>
import axios from 'axios';
import eventBus from '../EventBus.js';

export default {
    name : 'UpdatePage',
    props : ['contents'],
    data : function() {
        return { 
            no: this.contents.no, 
            name : this.contents.name, 
            title : this.contents.title,
            wrtdate : this.contents.wrtdate 
            }
    },
    methods : {
        updatemember : function() {
            axios({
                method : 'POST',
                url : '/updatemember',
                params : { no: this.no, 
                           name: this.name, 
                           title : this.title,
                           wrtdate : Date(this.wrtdate) }
            })
            .then((response) => {
                if(response.data == true) {
                    alert("수정 완료");
                    eventBus.$emit("complete");
                } else {
                    alert("수정 실패");
                }
            })
            .catch(() => {
                console.log('ERROR!!!');
            })
        }
    }
}
</script>