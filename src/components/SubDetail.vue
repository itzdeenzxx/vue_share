<template>
  <div>
    <div class="card my-2">
      <div class="card-body bg-dark bg-opacity-10">
        <h5 class="card-title">รหัสวิชา {{ subject.id }}</h5>
        <div class="card-sub-title">ชื่อวิชา {{ subject.name }}</div>
        <div class="cart-text">
          เกรดวิชา {{ subject.grade }} หน่วยกิต {{ subject.credit }}
        </div>
      </div>
    </div>
    <button class="btn btn-success" @click="editDetail">แก้ไขข้อมูล</button>
    &nbsp;
    <button class="btn btn-danger" @click="delDetail(stdId)">ลบข้อมูล</button>
    <div v-if="isEdit">
      <SubEdit :stdId="stdId" />
    </div>
  </div>
</template>

<script>
import SubEdit from "./SubEdit.vue"; // Import SubEdit component

export default {
  name: "SubDetail",
  props: ["stdId"],
  data() {
    return {
      subject: [],
      isEdit: false,
    };
  },
  mounted() {
    this.fetchStudentData();
  },
  methods: {
    fetchStudentData() {
      fetch(`http://localhost:3000/subject/${this.stdId}`)
        .then((res) => res.json())
        .then((data) => (this.subject = data))
        .catch((err) => console.log(err.message));
    },
    editDetail() {
      this.isEdit = !this.isEdit;
    },
    delDetail(theId) {
      fetch("http://localhost:3000/subject/" + theId, {
        method: "DELETE",
      })
        .then(() => {
          alert("ลบข้อมูลเรียบร้อยแล้ว");
          location.reload();
        })
        .catch((err) => console.log(err.message));
    },
  },
  components: {
    SubEdit, // Register SubEdit component
  },
};
</script>

<style>
/* Add your styles here */
</style>
