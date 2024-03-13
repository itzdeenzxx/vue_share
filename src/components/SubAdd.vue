<template>
    <div class="card">
        <div class="card-body">
            <form @submit.prevent="handleSubmit()">
                <div class="row">
                    <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
                        <label for="stdId" class="form-label">รหัสวิชา</label>
                        <input type="text" id="stdId" class="form-control" v-model.trim="sub.id" />
                    </div>
                    <div class="col-lg-8 col-md-8 col-sm-6 mt-2">
                        <label for="stdName" class="form-label">ชื่อวิชา</label>
                        <input type="text" id="stdName" class="form-control" v-model.trim="sub.name" />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="subgrade" class="form-label">เกรด</label>
                        <select id="subgrade" class="form-select" v-model="sub.grade">
                            <option value="1">A</option>
                            <option value="2">B+</option>
                            <option value="3">B</option>
                            <option value="4">C+</option>
                            <option value="5">C</option>
                            <option value="6">D+</option>
                            <option value="7">D</option>
                            <option value="8">F</option>
                            <option value="9">W</option>
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
                        <button id="btnSubmit" type="submit" class="btn btn-primary">บันทึก</button>
                    </div>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SubAdd',
    data() {
        return {
            sub: []
            
        }
    },
    methods: {
        handleSubmit() {
            let subject = {
                id: this.sub.id,
                name: this.sub.name,
                grade: this.sub.grade,
                credit: this.sub.credit,
                isShow: false
            }
            fetch('http://localhost:3000/subject', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(subject)
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