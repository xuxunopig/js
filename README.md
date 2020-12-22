# h5吊起支付宝app支付（前端）
初步按照支付宝官网会返回一个form表单
支付宝H5支付
async malipaynewPay() {


      // 这个接口是你们自己写的接口，成功后会返回一个form表单
       const wechatPay = await http.post(`${orderPay}`, {
         order_group:'order',
         pay_type: 2,
         user_price:this.user_price,
         trade_type: 'wap',
         order_id: this.orderInfo.order_id,


     })
     console.log(wechatPay)




      var el = document.createElement( 'div' );
      //wechatPay.data  就是后台返回的form表单
      console.log("wechatPay.data",wechatPay.data)


      el.innerHTML = wechatPay.data
      document.body.appendChild(el)
      document.forms[0].submit()


}
前面这种是大多数情况，还有一些情况，后台返回的不是表单表单，是个链接直接用这个链接拼也也可以调起

malipaynewPay() {
  // 里面的参数根据你们自己的数据填写即可
  // wechatPay.data 返回的链接


      let pay_url =
           wechatPay.data +
          "order_sn=" +
          this.orderInfo.order_id +
          "&body=" +
           this.goods_name +
          "&money=" +
          this.user_price +
          "&quit_url=" +
          window.location.href;
        console.log(pay_url);


       location.href = pay_url;
}


微信支付：微信内支付用sdk先判断是微信内浏览器还是微信外浏览器。
// 判断是否公众号（微信H5）
  isWechat() {
      // #ifdef H5
      const ua = window.navigator.userAgent.toLowerCase();
      if (ua.match(/micromessenger/i) == 'micromessenger') {
          return true;
      } else {
          return false;
      }
      // #endif
  },
  //支付


doPay() {
  if(this.isWechat()) {
      //微信浏览器
  } else {
    //微信外浏览器
    window.location.href = dataUrl
  }
}
微信外的只需要，这一步打开后台返回的链接即可
