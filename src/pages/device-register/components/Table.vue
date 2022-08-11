<template>
    <section>
        <div>
            <h1>Pano</h1>
            <button @click="sendPrinter" class="btn btn-secondary">
                <i class="fa fa-print" aria-hidden="true"></i>
                Yazdır</button>
            <button @click="createExcel" class="btn btn-secondary">
                <i class="fa fa-file-excel-o" aria-hidden="true"></i>
                Excel'e Aktar
            </button>
        </div>
        <table id="pano2" v-if="devices.length">
            <tr>
                <th v-for="title in titles">{{ title }}</th>
            </tr>
            <tr v-for="(device, index) in devices">
                <td><span class="spantd">{{ index + 1 }}</span></td>
                <td>{{ device.meditera }}</td>
                <td>{{ device.hospital }}</td>
                <td>{{ device.service }}</td>
                <td>{{ device.experienceCode }}</td>
                <td><button class="btn btn-danger btn-sm delete" @click="deleteDevice" type="button" title="Delete"><i
                            class="fa fa-trash"></i></button></td>
            </tr>
        </table>
    </section>
</template>

<script>
import { eventBus } from '../../../main'
export default {
    data() {
        return {
            titles: ["No", "Meditera", "Hastane", "Bölüm", "Hata Kodu", "Sil"],
            devices: [],
        }
    },
    created() {
        eventBus.$on("deviceAdded", (device) => {
            this.devices.push(device)
        })
    },
    methods: {
        createExcel() {
            function ExportToExcel(type, fn, dl) {
                var elt = document.getElementsByTagName('table')[0];
                var wb = XLSX.utils.table_to_book(elt, { sheet: "sheet1" });
                return dl ?
                    XLSX.write(wb, { bookType: type, bookSST: true, type: 'base64' }) :
                    XLSX.writeFile(wb, fn || ('MySheetName.' + (type || 'xlsx')));
            }
            ExportToExcel('xlsx');
        },
        deleteDevice(event) {
            const tr = event.currentTarget.parentNode.parentNode;
            const index = tr.firstChild.innerText;
            this.devices.splice(index - 1, 1)
        },
        //Yazdır Butonu
        sendPrinter() {
            var divToPrint = document.getElementById("print");
            var htmlToPrint = `
                <style type="text/css">
                    table, tr, th, td {
                        border:1px solid #999;
                        border-collapse: collapse;
                        padding:0.5em;
                    }
                </style>
            `
            htmlToPrint += divToPrint.outerHTML;
            newWin = window.open("");
            newWin.document.write(htmlToPrint);
            newWin.print();
            newWin.close();
        }
    },
    props: [],
    components: {

    },
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