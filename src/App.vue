
<template>
    <div>
        <navbar @historyList = "historyList" @payFormList = "payFormList" />
        <!--    отрендерить тот или иногй компонент-->
        <div v-if = "mainPage === 'historyPays'">
            <HistoryPay  :mainPage = 'mainPage' v-bind:dataPay = "dataPay" />
        </div>
        <div v-if = "mainPage === 'payForm'">
            <InvoiceForm  :mainPage = 'mainPage' v-bind:getInvoice = "getInvoice"  />
        </div>
        <div v-if = "mainPage === 'SuccesPayPage'">
            <SuccesPay  v-bind:dataPay = "dataPay" @historyList = "historyList"  />
        </div>
    </div>
</template>


<script>
import InvoiceForm from './components/InvoiceForm.vue'
import Navbar from './components/Navbar.vue'
import HistoryPay from './components/HistoryPay.vue'
import SuccesPay from './components/SuccesPay.vue'

export default {
    name: 'app',
    data() {
        return {
            mainPage: "payForm",
            dataPay: []
        }
    },
    components: {
        InvoiceForm,
        Navbar,
        HistoryPay,
        SuccesPay
    },
    methods: {
        historyList: function () {
            this.mainPage = "historyPays";
        },
        payFormList: function () {
            this.mainPage = "payForm";
        },
        getInvoice(numberInvoice,sumPay,userName, timePay) {
            this.dataPay.push({numberInvoice, sumPay, userName, timePay});
            this.mainPage = "SuccesPayPage";
        }
    }
}
</script>


