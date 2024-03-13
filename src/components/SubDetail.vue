<template>
    <div>
        <div class="card my-2">
            <div class="card-body bg-info bg-opacity-10">
                <h5 class="card-title">รหัสวิชา {{ subject.id }}</h5>
                <div class="card-sub-title">ชื่อวิชา {{ subject.name }}</div>
                <div class="cart-text">เกรดวิชา {{ subject.grade }} หน่วยกิต {{ subject.credit }}</div>
            </div>
        </div>
        <button class="btn btn-success" @click="editDetail">
            แก้ไขข้อมูล
        </button>
        &nbsp;
        <button class="btn btn-success" @click="delDetail(stdId)">
            ลบข้อมูล
        </button>
        <!-- เพิ่มส่วนนี้เพื่อเรียกใช้ SubEdit.vue -->
        <div v-if="isEdit">
            <SubEdit :stdId="stdId" />
        </div>
    </div>
</template>

<script>
import SubEdit from './SubEdit.vue'; // Import SubEdit component

export default {
    name: 'SubDetail',
    props: ['stdId'],
    data() {
        return {
            subject: [],
            isEdit: false
        };
    },
    mounted() {
        this.fetchStudentData();
    },
    methods: {
        fetchStudentData() {
            fetch(`http://localhost:3000/subject/${this.stdId}`)
                .then(res => res.json())
                .then(data => this.subject = data)
                .catch(err => console.log(err.message))
        },
        editDetail() {
            this.isEdit  =!this.isEdit;
        },
        delDetail(theId) {
            fetch('http://localhost:3000/subject/' + theId, {
                method: 'DELETE'
            })
            .then(() => {
                // Reload or perform any necessary actions after deletion
            })
            .catch(err => console.log(err.message))
        }
    },
    components: {
        SubEdit // Register SubEdit component
    }
};
</script>

<style>
/* Add your styles here */
</style>
