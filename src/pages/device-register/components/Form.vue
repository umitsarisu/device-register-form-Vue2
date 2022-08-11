<template>
    <form autocomplete="off">
        <h5>Cihaz Kayıt Formu</h5>
        <div class="formContainer">
            <div class="formContent">
                <p v-for="title in titles">{{ title }}</p>
            </div>
            <div class="formContent">
                <input type="text" v-model="device.meditera" class="form-control" placeholder="Meditera No" required
                    maxlength="5" tabindex="1" />
                <input list="hospitals" v-model="device.hospital" class="form-control" placeholder="Hastaneyi Girin"
                    required tabindex="2">
                <input list="departments" v-model="device.service" class="form-control" placeholder="Bölüm Girin"
                    tabindex="3">
                <input type="text" v-model="device.experienceCode" class="form-control" placeholder="Hata Kodu"
                    maxlength="5" tabindex="4" />
                <input type="submit" @click="sendToDevice" name="submit" class="form-control btn-danger" value="Gönder"
                    tabindex="5" />
                <datalist id="hospitals">
                    <option v-for="hospital in hospitals" :value="hospital[1]"></option>
                </datalist>
                <datalist id="departments">
                    <option v-for="department in departments" :value="department"></option>
                </datalist>
            </div>
        </div>
    </form>
</template>

<script>
import { eventBus } from '../../../main'
export default {
    data() {
        return {
            titles: ["Meditera:", "Hastane:", "Bölüm:", "Hata Kodu:"],
            device: {
                meditera: null,
                hospital: null,
                service: null,
                experienceCode: null,
            },
            hospitals: [],
            departments: [],
        }
    },
    methods: {
        sendToDevice() {
            if (this.device.meditera && this.device.hospital) {
                eventBus.$emit("deviceAdded", this.device)
                this.device = {
                    meditera: null,
                    hospital: null,
                    service: null,
                    experienceCode: null,
                }
            }
        }
    },
    created() {
        this.hospitals = privateHospitals.concat(istanbulHospitals).concat(outsideHospitals);
        this.departments = departments;
    }
}
</script>
<style scoped>
@media (min-width: 500px) {
    body {
        color: #212529;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
        -ms-flex-direction: column;
        flex-direction: column;
    }

    body form {
        width: 360px;
        margin: 40px auto 0;
        border: 2px solid #999;
        border-collapse: collapse;
        padding: 15px;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
        -ms-flex-direction: column;
        flex-direction: column;
    }

    body form h5 {
        border-bottom: 1px solid #555;
        margin-bottom: 5px;
    }

    body form .formContainer {
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: horizontal;
        -webkit-box-direction: normal;
        -ms-flex-direction: row;
        flex-direction: row;
        -webkit-box-pack: justify;
        -ms-flex-pack: justify;
        justify-content: space-between;
    }

    body form .formContainer .formContent {
        margin: 0 5px;
    }

    body form .formContainer .formContent input {
        margin: 7px 0;
    }

    body form .formContainer .formContent p {
        line-height: 38px;
        font-size: 18px;
        font-weight: bold;
        margin: 7px 0;
    }

    body section {
        width: 100%;
    }

    body section .panoHeader {
        margin: 10px;
    }

    body section table {
        width: 100%;
        border: 1px solid #999;
        border-radius: 10px;
    }

    body section table tr,
    body section table th,
    body section table td {
        border: 1px solid #999;
        padding: 5px;
    }

    body section table th:nth-child(1) {
        min-width: 30px;
    }

    body section table th:nth-child(2) {
        min-width: 80px;
    }

    body section table th:nth-child(3) {
        min-width: 160px;
    }

    body section table th:nth-child(4) {
        min-width: 100px;
    }

    body section table th:nth-child(5) {
        min-width: 80px;
    }

    body section table th:nth-child(6) {
        min-width: 30px;
    }
}

@media (min-width: 720px) {
    body section {
        width: 90%;
        margin: 0 auto;
    }

    body section table th:nth-child(3) {
        min-width: 300px;
    }

    body section table th:nth-child(4) {
        min-width: 200px;
    }

    body section table th:nth-child(5) {
        min-width: 92px;
    }

    body section table th:nth-child(6) {
        min-width: 32px;
    }
}

@media (min-width: 960px) {
    body {
        color: #212529;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
        -ms-flex-direction: column;
        flex-direction: column;
    }

    body form {
        width: 360px;
        margin: 60px 0 0 40px;
        border: 2px solid #999;
        border-collapse: collapse;
        padding: 15px;
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: vertical;
        -webkit-box-direction: normal;
        -ms-flex-direction: column;
        flex-direction: column;
    }

    body form h5 {
        padding: 5px;
        margin-bottom: 5px;
        border-bottom: 1px solid #555;
    }

    body form .formContainer {
        display: -webkit-box;
        display: -ms-flexbox;
        display: flex;
        -webkit-box-orient: horizontal;
        -webkit-box-direction: normal;
        -ms-flex-direction: row;
        flex-direction: row;
        -webkit-box-pack: justify;
        -ms-flex-pack: justify;
        justify-content: space-between;
    }

    body form .formContainer .formContent {
        margin: 0 5px;
    }

    body form .formContainer .formContent input {
        margin: 7px 0;
    }

    body form .formContainer .formContent p {
        line-height: 38px;
        font-size: 18px;
        font-weight: bold;
        margin: 7px 0;
    }

    body section {
        width: 90%;
        margin: 0 40px;
    }

    body section .panoHeader {
        margin: 10px;
    }

    body section table {
        border: 1px solid #999;
    }

    body section table tr,
    body section table th,
    body section table td {
        border: 1px solid #999;
        padding: 5px;
    }

    body section table th:nth-child(3) {
        min-width: 300px;
    }

    body section table th:nth-child(4) {
        min-width: 200px;
    }

    body section table th:nth-child(5) {
        min-width: 92px;
    }

    body section table th:nth-child(6) {
        min-width: 32px;
    }
}

/*# sourceMappingURL=style.css.map */
</style>