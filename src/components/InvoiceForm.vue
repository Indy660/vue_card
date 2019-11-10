<template>
  <div class="container-fluid py-3">
    <div class="row">
      <div class="col-12 col-sm-8 col-md-6 col-lg-4 mx-auto">
        <div  class="card">
          <div class="card-body">
            <div class="card-title">
              <h3 class="text-center">Заполните данные для оплаты</h3>
            </div>
            <hr>
            <b-form action="/echo" method="post" @submit.stop.prevent>

              <label>Номер счёта</label>
              <b-input v-model="numberInvoice" @keypress=justNumbers></b-input>

              <label>Сумма оплаты (в рублях)</label>
              <b-input v-model="sumPay" @keypress=justNumbers></b-input>

              <label>Имя держателя карты</label>
              <b-input v-model="userName" @keypress=justLatinInput :state="validationName"></b-input>
              <b-form-invalid-feedback :state="validationName">
                Введите имя латиницей, как минимум 4 буквы
              </b-form-invalid-feedback>
              <b-form-valid-feedback :state="validationName">
                Форма заполнена верно
              </b-form-valid-feedback>

              <label class="control-label mb-1">Номер карты</label>
              <div class="row">
                <div class="col-3">
                  <b-input v-model="userCardPath1" :state="validationCard1" @keypress=justNumbers maxlength="4"></b-input>
                  <b-form-invalid-feedback :state="validationCard1">
                    Введите 4 цифры
                  </b-form-invalid-feedback>
                </div>
                <div class="col-3">
                  <b-input v-model="userCardPath2" :state="validationCard2" @keypress=justNumbers maxlength="4"></b-input>
                  <b-form-invalid-feedback :state="validationCard2">
                    Введите 4 цифры
                  </b-form-invalid-feedback>
                </div>
                <div class="col-3">
                  <b-input v-model="userCardPath3" :state="validationCard3" @keypress=justNumbers  maxlength="4" ></b-input>
                  <b-form-invalid-feedback :state="validationCard3">
                    Введите 4 цифры
                  </b-form-invalid-feedback>
                </div>
                <div class="col-3">
                  <b-input v-model="userCardPath4" :state="validationCard4" @keypress=justNumbers maxlength="4" ></b-input>
                  <b-form-invalid-feedback :state="validationCard4">
                    Введите 4 цифры
                  </b-form-invalid-feedback>
                </div>
              </div>

              <div class="row">
                <div class="col-6">
                  <label class="control-label mb-1">Срок действия</label>
                    <b-input v-model="userDate" :state="validationDate" placeholder="MM / YY"  maxlength="5" @keypress=justNumbers @input=addSymbol  ></b-input>
                    <b-form-invalid-feedback :state="validationDate">
                      Введите даты
                    </b-form-invalid-feedback>
                </div>

                <div class="col-6">
                  <label class="control-label mb-1">Код на обратной стороне</label>
                  <b-input v-model="userCVV" :state="validationCVV" maxlength="3" @keypress=justNumbers ></b-input>
                  <b-form-invalid-feedback :state="validationCVV">
                    Введите код
                  </b-form-invalid-feedback>
                </div>
              </div>

              <div>
                <button type="submit" class="btn btn-lg btn-info btn-block"  v-on:click="sendInvoice">Оплатить</button>
              </div>
            </b-form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  export default {
    name: "InvoiceForm",
    props:["getInvoice"],
    data() {
      return {
        numberInvoice: '',
        sumPay: '',
        userName: '',
        userCardPath1: '',
        userCardPath2: '',
        userCardPath3: '',
        userCardPath4: '',
        userDate: "",
        userCVV: "",
      }
    },
    computed: {
      validationName() {
        return this.userName.length > 4
      },
      validationCard1() {
        return this.userCardPath1.length === 4
      },
      validationCard2() {
        return this.userCardPath2.length === 4
      },
      validationCard3() {
        return this.userCardPath3.length === 4
      },
      validationCard4() {

        return this.userCardPath4.length === 4
      },
      validationDate() {
        return this.userDate.length === 5
      },

      validationCVV() {
        return this.userCVV.length === 3
      }
    },
    methods: {
      justLatinInput: function (e) {
        // console.log(e.key);
        if ( (!/[a-z]/i.test(e.key)))                         // Проверка на разрешённые символы
             //(!/[[:space:]]/.test(e.key))  )                     // Проверка на количество пробелов
           e.preventDefault();                                // Если условие выполнилось, то запрещаем ввод символа
         // else {
         //  console.log(e.key)
         //  console.log(/[a-z]/i.test(String.fromCharCode(e.key)))
         // }
      },
      justNumbers: function (e) {
        // console.log(e.key);
        if ((!/[0-9]/.test(e.key)))                         // Проверка на разрешённые символы
          e.preventDefault();
      },
      sendInvoice: function () {
        if ((this.numberInvoice.length !== 0) &&
            (Number(this.sumPay) > 0) &&
            (this.userName.length > 4) &&
            (this.userCardPath1.length === 4) &&
            (this.userCardPath2.length === 4) &&
            (this.userCardPath3.length === 4) &&
            (this.userCardPath4.length === 4) &&
            (this.userDate.length === 5) &&
            (this.userCVV.length === 3) ) {
          let timePay = Date.now();
          this.getInvoice(this.numberInvoice,this.sumPay,this.userName, timePay);
          this.numberInvoice = "";
          this.sumPay = "";
        }
      },
      addSymbol: function () {
        if ( this.userDate.length === 2) {
          return  this.userDate += "/"
        }
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






<!--<div class="form-group has-success">-->
<!--<label  class="control-label mb-1">Имя держателя карты</label>-->
<!--<input  type="text" class="form-control ">-->
<!--</div>-->

<!--<div class="row">-->
<!--<div class="col-3">-->
<!--<div class="form-group">-->
<!--<input  class="form-control" required="" maxlength="4">-->
<!--</div>-->
<!--</div>-->
<!--<div class="col-3">-->
<!--<div class="form-group">-->
<!--<input  class="form-control" required="" maxlength="4">-->
<!--</div>-->
<!--</div>-->
<!--<div class="col-3">-->
<!--<div class="form-group">-->
<!--<input  class="form-control" required="" maxlength="4">-->
<!--</div>-->
<!--</div>-->
<!--<div class="col-3">-->
<!--<div class="form-group">-->
<!--<input  class="form-control" required="" maxlength="4">-->
<!--</div>-->
<!--</div>-->


<!--<div class="col-6">-->
<!--<div class="form-group">-->
<!--<label class="control-label mb-1">Срок действия</label>-->
<!--<input  class="form-control"  placeholder="MM / YY">-->
<!--</div>-->
<!--</div>-->
<!--<div class="col-6">-->
<!--<label  class="control-label mb-1">Код на обратной стороне</label>-->
<!--<div class="input-group">-->
<!--<input  class="form-control" maxlength="3">-->
<!--</div>-->
<!--</div>-->
<!--</div>-->