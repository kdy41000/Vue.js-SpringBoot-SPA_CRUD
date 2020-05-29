<template>
    <div>
        이름 : <input type="text" v-model.trim="name" />
        제목 : <input type="text" v-model.trim="title" />
        <button @click="insertmember">등록</button>
    </div>
</template>
<script>
import axios from 'axios';
import eventBus from '../EventBus.js';

export default {
    name : 'InsertPage',
    data : function() {
        return { name : '', title : '' }
    },
    methods : {
        insertmember : function() {
            axios({
                method : 'POST',
                url : '/insertmember',
                params : { name: this.name, title : this.title }
            })
            .then((response) => {
                if(response.data == true) {
                    alert("등록 완료");
                    eventBus.$emit("complete");
                } else {
                    alert("등록 실패");
                }
            })
            .catch(() => {
                console.log('ERROR!!!');
            })
        }
    }
}
</script>