<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta content="telephone=no" name="format-detection">
    <meta content="email=no" name="format-detection">
    <meta name="author" content="mr.heyong@foxmail.com">
    <title>二维码支付</title>
    <script>
        var docEl=document.documentElement;var dpr=window.devicePixelRatio||1;function refreshRem(){var width=document.documentElement.getBoundingClientRect().width;if(width>740){width=740}var rem=width/7.5;document.documentElement.style.fontSize=rem+"px"}refreshRem();window.addEventListener("resize",refreshRem);window.addEventListener("pageshow",function(e){if(e.persisted){refreshRem()}});docEl.classList.add("dpr-"+dpr);
        if(dpr>=2){var fakeBody=document.createElement("body");var testElement=document.createElement("div");testElement.style.border=".5px solid transparent";fakeBody.appendChild(testElement);docEl.appendChild(fakeBody);if(testElement.offsetHeight===1){docEl.classList.add("hairlines")}docEl.removeChild(fakeBody)};
    </script>
    <style>
        [v-cloak]{
            display: none;
        }
        body{
            margin: 0;
            padding: 0;
            font-size: 14px;
            background-color: #F7F7F9;
            font-family: PingFangSC-Regular;
        }
        .wrap{
            margin: 15px;
            padding: 0;
        }
        .wrap img{
            position: fixed;
            left: 0;
            top: 0;
            width: 100%;
            height: 50%;
            z-index: 2;
            opacity: 0;
        }
        .wrap .code{
            max-width: 345px;
            height: 260px;
            background-color: #fff;
        }
        .wrap .code .head{
            display: flex;
            flex-direction: column;
            padding: 15px 15px 0 15px;
            height: 70px;
        }
        .wrap .code .head .title{
            font-size: 16px;
            color: #313133;
            letter-spacing: 0;
            font-weight: 600;
            line-height: 20px;
            max-width: 266px;
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
        }
        .wrap .code .head .norm{
            margin: 8px 0;
            display: flex;
            justify-content: space-between;
        }
        .wrap .code .head .norm span{
            display: block;
        }
        .wrap .code .head .norm span:first-child{
            font-size: 14px;
            color: #757577;
            text-align: center;
            line-height: 22px;
        }
        .wrap .code .head .norm span:last-child{
            font-size: 18px;
            color: #FFA000;
            text-align: center;
            line-height: 22px;
            font-weight: 600;
        }
        .wrap .code .head i{
            display: block;
            max-width: 311px;
            height: 1px;
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/border@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .code .qr-code{
            width: 100px;
            height: 100px;
            margin: 0 auto;
            background-color: #313133;
        }
        .wrap .code .qr-code img{
            width: 100px;
            height: 100px;
        }
        .wrap .code .qr-btn{
            margin: 15px;
            max-width: 315px;
            height: 45px;
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/btn@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step{
            margin: 15px 0;
        }
        .wrap .explanation .step .num {
            display: inline-flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
        }
        .wrap .explanation .step .num span{
            display: block;
            width: 30px;
            height: 30px;
            border-radius: 50%;
        }
        .wrap .explanation .step .num span:nth-child(1){
            margin-left: 5px;
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/circle@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step .num span:nth-child(3){
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/copy 2@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step .num span:nth-child(5){
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/copy 3@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step .num span:nth-child(7){
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/copy 4@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step .num span:nth-child(9){
            margin-right: 15px;
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/copy@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step .num i{
            display: block;
            width: 30px;
            height: 1px;
            background-image: url('http://valar.ixiaolu.com/h5/qr-img/border@3x.png');
            background-size: 100% 100%;
            background-repeat: no-repeat;
        }
        .wrap .explanation .step .font{
            display: inline-flex;
            justify-content: space-between;
            margin-top: 9px;
            font-size: 11px;
            color: #108EE9;
        }
        .wrap .explanation .detailed{
            display: flex;
            flex-direction: column;
        }
        .wrap .explanation .detailed span{
            line-height: 20px;
            margin-top: 10px;
        }
        .wrap .explanation .detailed span a{
            text-decoration:none; 
            color: #108EE9;
            font-weight: 600;
        }
    </style>
</head>
<body>

    <div id="app" class="wrap">
        <img :src="img" alt="">
        <div class="code">
            <div class="head">
                <div class="title">真爱课堂-挽回爱情高级私人定制指…真爱课堂-挽回爱情高级私人定制指…</div>
                <div class="norm">
                    <span>规格1</span>
                    <span>￥3998</span>
                </div>
                <i></i>
            </div>
            <div class="qr-code"><img :src="img" alt="" id="img"></div>
            <div class="qr-btn" @touchstart="saveImg()"></div>
        </div>
        <div class="explanation">
            <div class="step">
                <div class="num">
                    <span></span>
                    <i></i>
                    <span></span>
                    <i></i>
                    <span></span>
                    <i></i>
                    <span></span>
                    <i></i>
                    <span></span>
                </div>
                <div class="font">
                    <span>保存图片  &nbsp;二维码</span>
                    <span>&nbsp;&nbsp;打开支付宝 &nbsp;"扫一扫"识别</span>
                    <span>输入金额 完成付款</span>
                    <span>&nbsp;&nbsp;复制订单号&nbsp;&nbsp;&nbsp;&nbsp; 发送给咨询师</span>
                    <span>&nbsp;&nbsp;&nbsp;咨询师 &nbsp;绑定订单</span>
                </div>
            </div>
            <div class="detailed">
                <span>1、由于微信无法处理支付宝请求，请保存二维码后打开支付宝“扫一扫”完成付款；</span>
                <span>2、完成付款后，<b>请复制订单号（支付宝-我的-账单）发送给咨询师</b>；</span>
                <span>3、订单在咨询师绑定成功后正式生效，点击<a href="">查询交易</a>可以查看结果；</span>
                <span>4、如确认已支付却未查到交易记录，请联系咨询师进行绑单操作；</span>
            </div>
        </div>
    </div>

    <script src="https://valar.ixiaolu.com/common/lib/vue.min.js"></script>
    <script>
        var app = new Vue({
            el: '#app',
            data: {
                img:'http://valar.ixiaolu.com/h5/qr-img/btn@3x.png'
            },
            methods: {
                saveImg: function(){
                    alert(1)
                    let timer = null
                    let startTime = ''
                    let endTime = ''
                    const label = document.querySelector('.wrap>img');

                    label.addEventListener('touchstart', function () {
                        startTime = +new Date()
                    })

                    label.addEventListener('touchend', function () {
                        endTime = +new Date()
                        clearTimeout(timer)
                        if (endTime - startTime < 700) {
                            // 处理点击事件
                            this.saveImg;
                        }
                    })
                }
            }
        });
    </script>
</body>
</html>
