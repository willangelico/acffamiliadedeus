<template>
  <div id="app">
    <div class="content">
      <div class="logo">
        <h1>
          <img alt="ACF Família de Deus" class="text-center" src="static/imgs/logo.png" />
        </h1>
      </div>
      <div class="box-doacao">
        <h2 class="text-center" >Faça sua doação</h2>
        <p>Escolha o valor e pague com VISA Checkout</p>
        <div class="iptValue">
          <span>R$</span>
          <input type="text" v-model="paymentRequest.subtotal">
        </div>
        <img alt="Visa Checkout" class="v-button text-center" role="button" src="https://sandbox.secure.checkout.visa.com/wallet-services-web/xo/button.png" />
      </div>
    </div>
    <div class="footer">
      © 2018 - Acffd - Todos os Direitos Reservados.
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data () {
    return {
      apikey: '543XH5BJL766EQVPE06B21ASrhW8i076TDvhkVhZa7FfJl8R8',
      paymentRequest: {
        currencyCode: 'BRL',
        subtotal: '15.00'
      }
    }
  },

  created: function () {
    let visa = document.createElement('script')
    visa.setAttribute('src', '//sandbox-assets.secure.checkout.visa.com/checkout-widget/resources/js/integration/v1/sdk.js')
    document.head.appendChild(visa)
  },

  mounted: function () {
    setTimeout(() => {
      V.init({
        apikey: this.apikey,
        paymentRequest: this.paymentRequest
      })
      V.on('payment.success', function (payment) { alert(JSON.stringify(payment)) })
      V.on('payment.cancel', function (payment) { alert(JSON.stringify(payment)) })
      V.on('payment.error', function (payment, error) { alert(JSON.stringify(error)) })
    }, 2000)
  }
}
</script>

<style>
body{
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #888888;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
}

.box-doacao {
  background: #EDEDED;
  max-width: 400px;
  padding: 20px;
  border-radius: 10px;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.iptValue {
  margin: 20px;
}

.iptValue input {
  height: 20px;
  border: 1px solid #CCC;
}

.footer{
  background: #727272;
  color: white;
  font-size: 12px;
  padding: 10px;
}
</style>
