<template>
  <div  class="container py-5 text-center">
    <table class="table table-dark">
      <thead>
      <tr>
        <th scope="col">№</th>
        <th scope="col">Номер платежа</th>
        <th scope="col">Сумма оплаты</th>
        <th scope="col">Имя</th>
        <th scope="col">Время отправки</th>
      </tr>
      </thead>
      <tbody>

      <tr  v-for= '(positionInvoice, index) in dataPay' :key='index'>
        <td>{{index+1}}</td>
        <td>{{positionInvoice.numberInvoice}}</td>
        <td>{{positionInvoice.sumPay}} руб</td>
        <td>{{positionInvoice.userName}}</td>
        <td>{{getTime(positionInvoice.timePay)}}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import moment from "moment"

  export default {
    name: "HistoryPay",
    props: ['dataPay'],
    data: ()=>({

    }),
    methods: {
      getTime (timeMessage) {
        moment.lang('ru');
        return moment(timeMessage).format('LLL')
      },
    }
  }
</script>