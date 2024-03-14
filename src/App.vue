<template>
  <div class="main">
    <h1 class="display-5 title-port">PORTFOLIO</h1>

    <h1 class="display-6">{{ name }}</h1>
    <div class="banner-profile">
      <div>
        <img src="./assets/addeen2.png" class="image-me" alt="" />
      </div>
    </div>
    <br /><br />
    <p class="description-profile">{{ des }}</p>
    <p class="hobbies-profile">{{ hobbies }}</p>
    
    <h3 class="std-result">ผลการเรียน</h3>
    <button class="btn-std" @click="toggleAdd()">เพิ่มผลการเรียน</button>
    <button class="btn-std" @click="toggleList()">แสดงผลการเรียน</button>

    <div class="m-5 p-1" v-if="showSubAdd">
      <SubAdd/> 
    </div>
    <br><br>
    <div class="m-5 p-1" v-if="showSubList">
      <SubList :students="students" />
    </div>
    <div class="m-2" v-if="showSubEdit">
      <SubEdit :stdId="someIdHere" />
    </div>
  </div>
</template>

<script>
import SubAdd from "./components/SubAdd";
import SubList from "./components/SubList";

export default {
  name: "App",
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
    };
  },
  mounted() {
    fetch("http://localhost:3000/data_port")
      .then((res) => res.json())
      .then((data) => {
        if (Array.isArray(data) && data.length > 0) {
          const student = data[0];
          this.name = student.name || "ไม่พบข้อมูล";
          this.des = student.des || "ไม่พบข้อมูล";
          this.hobbies = student.hobbies || "ไม่พบข้อมูล";
          this.image = student.image || "ไม่พบข้อมูล";
          this.students = data;
        } else {
          this.name = "ไม่พบข้อมูล";
          this.major = "ไม่พบข้อมูล";
          this.des = "ไม่พบข้อมูล";
        }
      })
      .catch((err) => console.log(err.message));

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
body {
  background-image: url(./assets/bg.jpg);
}

.main {
  font-family: "Prompt", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
.title-port {
  background: linear-gradient(45deg, #f00, #ff0, #0f0, #0ff, #00f, #f0f, #f00);
  background-size: 200% 200%;
  animation: rainbow 3s linear infinite;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 400;
}

@keyframes rainbow {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}


.banner-profile {
}

.image-me {
  border-radius: 16px;
  /* box-shadow: 0px -2px 6px 5px rgba(0, 0, 0, 0.1); */
}

.description-profile {
  /* margin: 20px; */
  margin-left: 40px;
  margin-right: 40px;
  font-size: 30px;
}

.hobbies-profile {
  font-size: 18px;
}

.btn-std {
  margin: 10px;
  --b: 3px;
  --s: 0.45em;
  --color: #373b44;
  padding: calc(0.5em + var(--s)) calc(0.9em + var(--s));
  color: var(--color);
  --_p: var(--s);
  background: conic-gradient(
      from 90deg at var(--b) var(--b),
      #0000 90deg,
      var(--color) 0
    )
    var(--_p) var(--_p) / calc(100% - var(--b) - 2 * var(--_p))
    calc(100% - var(--b) - 2 * var(--_p));
  transition: 0.3s linear, color 0s, background-color 0s;
  outline: var(--b) solid #0000;
  outline-offset: 0.6em;
  font-size: 16px;

  border: 0;

  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.btn-std:hover,
.btn-std:focus-visible {
  --_p: 0px;
  outline-color: var(--color);
  outline-offset: 0.05em;
  
}

.btn-std:active {
  background: var(--color);     
  color: #fff;
}


</style>
