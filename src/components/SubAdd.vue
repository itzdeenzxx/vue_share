<template>
    <div class="card">
        <div class="card-body">
            <form @submit.prevent="handleSubmit()">
                <div class="row">
                    <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
                        <label for="stdId" class="form-label">รหัสวิชา</label>
                        <input type="text" id="stdId" class="form-control" v-model.trim="stds.id" />
                    </div>
                    <div class="col-lg-8 col-md-8 col-sm-6 mt-2">
                        <label for="stdName" class="form-label">ชื่อวิชา</label>
                        <input type="text" id="stdName" class="form-control" v-model.trim="stds.name" />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="stdYr" class="form-label">เกรด</label>
                        <select id="stdYr" class="form-select" v-model="stds.yr">
                            <option value="1">A</option>
                            <option value="2">B+</option>
                            <option value="3">B</option>
                            <option value="4">C+</option>
                            <option value="4">C</option>
                            <option value="4">D+</option>
                            <option value="4">D</option>
                            <option value="4">F</option>
                            <option value="4">W</option>
                        </select>
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="stdYr" class="form-label">หน่วยกิต</label>
                        <select id="stdYr" class="form-select" v-model="stds.yr">
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                            <option value="4">4</option>
                        </select>
                    </div>
                    <div class="col-2 mt-4 d-flex align-item-center">
                        <button id="btnSubmit" type="submit" class="btn btn-primary">บันทึก</button>
                    </div>
                </div>
            </form>

        </div>
    </div>
    <div class="alert alert-success mt-2" v-show="addSuccess">
    บันทึกข้อมูล {{ stds.id }} - {{ stds.name }} สำเร็จ
    </div>
    <div class="alert alert-danger mt-2" v-shoe="addError">
    {{ errMessage }}
    </div>
</template>

<script>
export default {
    name: 'SubAdd',
    data() {
        return {
            stds: {
                id: "",
                name: "",
                major: "CS",
                yr: 2,
                inshow: false
            }
        }
    },
    methods: {
        handleSubmit() {
            let students = {
                id: this.stds.id,
                name: this.stds.name,
                major: this.stds.major,
                yr: this.stds.yr,
                isShow: false
            }
            fetch('http://localhost:3000/students', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(students)
            })
                .then(() => {
                    this.addSuccess = true
                })
                .catch((err) => {
                    this.addError = true
                    this.errMessage = err
                })
        }

    }
}
</script>

<style></style>