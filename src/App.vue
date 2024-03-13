<template>
  <div>
    <h1 class="display-5 text-primary">Portfolio</h1>
    
    <h1 class="display-6 text-primary">{{ name }}</h1>
    <img src="./assets/addeen.png" alt="">
    <p class="text-danger text-opacity-50">{{ des }}</p>
    <p class="text-danger">{{ hobbies }}</p>
    
    <p>ผลการเรียน</p>
    <button class="btn btn-outline-primary btn-sm mx-1" @click="toggleAdd()">เพิ่มผลการเรียน</button>
    <button class="btn btn-outline-secondary btn-sm mx-1" @click="toggleList()">แสดงผลการเรียน</button>
    
    <div class="m-2" v-if="showSubAdd">
      <SubAdd/> 
    </div>
    <br><br>
    <div class="m-2" v-if="showSubList">
      <SubList :students="students" />
    </div>
    <div class="m-2" v-if="showSubEdit">
      <SubEdit :stdId="someIdHere" />
    </div>
    
  </div>
</template>

<script>
import SubAdd from './components/SubAdd'
import SubList from './components/SubList'

export default {
  name: 'App',
  components: {
    SubList,
    SubAdd,
  },
  data() {
    return {
      name: "",
      major: "",
      des: "",
      hobbies : "",
      image:"",
      showSubList: false,
      showSubAdd: false,
      showSubEdit: false,
      students: [],
      someIdHere: 123
    }
  },
  mounted() {
    fetch('http://localhost:3000/data_port')
        .then(res => res.json())
        .then(data => {
          if (Array.isArray(data) && data.length > 0) {
            const student = data[0];
            this.name = student.name || 'ไม่พบข้อมูล';
            this.des = student.des || 'ไม่พบข้อมูล';
            this.hobbies = student.hobbies || 'ไม่พบข้อมูล';
            this.image = student.image || 'ไม่พบข้อมูล';
            this.students = data;
          } else {
            this.name = 'ไม่พบข้อมูล';
            this.major = 'ไม่พบข้อมูล';
            this.des = 'ไม่พบข้อมูล';
          }
        })
        .catch(err => console.log(err.message))
  },
  methods: {
    toggleList() {
      this.showSubList = !this.showSubList;
      this.showSubAdd = false;
      this.showSubEdit = false;
    },
    toggleAdd() {
      this.showSubAdd = !this.showSubAdd;
      this.showSubList = false;
      this.showSubEdit = false;
    },
    toggleEdit() {
      this.showSubEdit = !this.showSubEdit;
      this.showSubList = false;
      this.showSubAdd = false;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
