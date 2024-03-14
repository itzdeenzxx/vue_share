<template>
  <div class="card">
    <div class="card-body">
      <form @submit.prevent="handleSubmit()">
        <div class="row">
          <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
            <label for="stdId" class="form-label">รหัสวิชา</label>
            <input
              type="text"
              id="stdId"
              class="form-control"
              v-model.trim="sub.id"
            />
          </div>
          <div class="col-lg-8 col-md-8 col-sm-6 mt-2">
            <label for="stdName" class="form-label">ชื่อวิชา</label>
            <input
              type="text"
              id="stdName"
              class="form-control"
              v-model.trim="sub.name"
            />
          </div>
          <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
            <label for="subgrade" class="form-label">เกรด</label>
            <select id="subgrade" class="form-select" v-model="sub.grade">
              <option value="A">A</option>
              <option value="B+">B+</option>
              <option value="B">B</option>
              <option value="C+">C+</option>
              <option value="C">C</option>
              <option value="D+">D+</option>
              <option value="D">D</option>
              <option value="F">F</option>
              <option value="W">W</option>
            </select>
          </div>
          <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
            <label for="subCre" class="form-label">หน่วยกิต</label>
            <select id="subCre" class="form-select" v-model="sub.credit">
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
            </select>
          </div>
          <div class="col-2 mt-4 d-flex align-item-center">
            <button id="btnSubmit" type="submit" class="btn btn-secondary btnSave">
              บันทึก
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "SubAdd",
  data() {
    return {
      sub: [],
    };
  },
  methods: {
    handleSubmit() {
      let subject = {
        id: this.sub.id,
        name: this.sub.name,
        grade: this.sub.grade,
        credit: this.sub.credit,
        isShow: false,
      };
      fetch("http://localhost:3000/subject", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(subject),
      })
        .then(() => {
            
          this.addSuccess = true;
        })
        .catch((err) => {
          this.addError = true;
          this.errMessage = err;
        });
    },
  },
};
</script>

<style>


/* button */
.btnSave {
  padding: 0.6em 2em;
  border: none;
  outline: none;
  color: rgb(255, 255, 255);
  background: #111;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 10px;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.btnSave:before {
  content: "";
  background: linear-gradient(
    45deg,
    #ff0000,
    #ff7300,
    #fffb00,
    #48ff00,
    #00ffd5,
    #002bff,
    #7a00ff,
    #ff00c8,
    #000000
  );
  position: absolute;
  top: -2px;
  left: -2px;
  background-size: 400%;
  z-index: -1;
  filter: blur(5px);
  -webkit-filter: blur(5px);
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  animation: glowing-button-85 20s linear infinite;
  transition: opacity 0.3s ease-in-out;
  border-radius: 10px;
}

@keyframes glowing-button-85 {
  0% {
    background-position: 0 0;
  }
  50% {
    background-position: 400% 0;
  }
  100% {
    background-position: 0 0;
  }
}

.btnSave:after {
  z-index: -1;
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  background: #222;
  left: 0;
  top: 0;
  border-radius: 10px;
}
</style>