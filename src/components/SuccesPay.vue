<template>
  <div class="container-fluid py-3">
    <div class="row">
      <div class="col-12 col-sm-8 col-md-6 col-lg-4 mx-auto">
        <div id="pay-invoice" class="card">
          <div class="card-body">
            <div class="card-title">
              <h3 class="text-center">Счёт успешно оплачен!</h3>
            </div>
            <hr>

            Счет {{lastPay.numberInvoice}} оплачен, владелец карты {{lastPay.userName}} заплатил {{lastPay.sumPay}} рубля. <br>
            Дата оплаты: {{getTime(lastPay.timePay)}}

            <div>
              <button type="submit" class="btn btn-lg btn-info btn-block"  v-on:click="returnHomePage">Вернуться к истории оплаченных счетов</button>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import moment from "moment"

  export default {
    name: "SuccesPay",
    props: ['dataPay'],
    data() {
      return {

      }
    },

    computed: {
      lastPay: function () {
        return this.dataPay[this.dataPay.length - 1]
      }
    },
      methods: {
        returnHomePage: function () {
          this.$emit("historyList")
        },
        getTime(timeMessage) {
          moment.lang('ru');
          return moment(timeMessage).format('LLL')
        }
      }
    }

</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
div {
  margin: 5px 0 0;
}

button {
  margin: 50px 0 0;
}

</style>




