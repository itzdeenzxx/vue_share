<template>
  <div>
      <h2>แก้ไขข้อมูลนิสิต</h2>
      <form @submit.prevent="handleSubmit">
          <div class="mb-3">
              <label for="editName" class="form-label">รหัสวิชา</label>
              <input type="text" class="form-control" id="editName" v-model="editedStudent.id">
          </div>
          <div class="mb-3">
              <label for="editName" class="form-label">ชื่อวิชา</label>
              <input type="text" class="form-control" id="editName" v-model="editedStudent.name">
          </div>
          <div class="mb-3">
              <label for="editMajor" class="form-label">เกรด</label>
              <input type="text" class="form-control" id="editMajor" v-model="editedStudent.grade">
          </div>
          <div class="mb-3">
              <label for="editYear" class="form-label">หน่วยกิต</label>
              <input type="number" class="form-control" id="editYear" v-model="editedStudent.credit">
          </div>
          <button type="submit" class="btn btn-primary">บันทึกการแก้ไข</button>
      </form>
  </div>
</template>

<script>
export default {
  name: 'SubEdit',
  props: ['stdId'],
  data() {
      return {
          editedStudent: []
      };
  },
  mounted() {
      this.fetchStudentData();
  },
  methods: {
      fetchStudentData() {
          fetch(`http://localhost:3000/subject/${this.stdId}`)
              .then(response => response.json())
              .then(data => {
                  this.editedStudent = data;
              })
              .catch(error => {
                  console.error('Error fetching student data:', error);
              });
      },
      handleSubmit() {
          fetch(`http://localhost:3000/subject/${this.stdId}`, {
              method: 'PUT',
              headers: {
                  'Content-Type': 'application/json'
              },
              body: JSON.stringify(this.editedStudent)
          })
          .then(() => {
              alert('บันทึกการแก้ไขข้อมูลเรียบร้อยแล้ว');
              location.reload()
          })
          .catch(error => {
              console.error('Error updating student data:', error);
              alert('เกิดข้อผิดพลาดในการบันทึกการแก้ไขข้อมูล');
          });
      }
  }
};
</script>

<style>
/* สไตล์ต่าง ๆ สำหรับฟอร์มแก้ไขข้อมูล หรือตามต้องการ */
</style>
