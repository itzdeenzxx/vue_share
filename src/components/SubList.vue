<template>
    <div>
        <h2>ผลการเรียน</h2>
        <ul class="list-group">
            <li v-for="(std, id) in subject" :key="id" class="list-group-item">
                
                <a href="#" @click="setShow(std)">
                    {{ std.name }}
                </a>
                <div v-if="std.isShow">
                    <SubDetail :stdId="std.id" @edit="showEdit" @delete="reload()"/>
                </div>
            </li>
            <div v-if="isEdit">
                {{ EditId }}
            </div>
        </ul>
        <br><br>
    </div>
</template>

<script>
import SubDetail from './SubDetail.vue';
export default {
    name: 'SubList',
    components:{
        SubDetail
    },
    data() {
        return {
            subject: [],
            isEdit : false,
            EditId : '',
        };
    },
    mounted(){
        fetch('http://localhost:3000/subject')
        .then(res=>res.json())
        .then(data=>this.subject=data)
        .catch(err=>console.log(err.message))
    },
    methods:{
        setShow(theId){
            theId.isShow = !theId.isShow
            
        },
        showEdit(theStdId){
            this.EditId = theStdId
            this.isEdit = true
        },
        reload(){
            this.$parent.showSubList = !this.$parent.showSubList 
        }
    }
};
    

</script>

<style>
/* Add your styles here */
</style>
