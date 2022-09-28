<template>
    <div class="app">
        <button class="main-but" v-if="!popUp.isVisible" @click="popUp.isVisible = !popUp.isVisible">Open Pop-Up</button>
        <div class="pop-up" v-if="popUp.isVisible">
            <div class="img-block">
                <div class="cross-but" @click="popUp.isVisible = !popUp.isVisible; popUp.alert.state =''"></div>
            </div>
            <div class="percent">10%<span>off</span></div>
            <div class="first-order">
                <span>your firs order</span>
                <hr>
                <p>Subscrive to recieve 10% off promocode plus exclusive offers and deals</p>
            </div>
            <div class="alert" v-if="popUp.alert.state != ''" :class="popUp.alert.state">{{popUp.alert.message}}</div>
            <div class="email">
                <span>Email-adress</span>
                <input type="text"  v-model="popUp.input.value">
                <button @click="subscribeHandler">Subscribe!</button>
                <div class="i-am-agree">
                    <div class="checkbox" @click="checkBoxChangeState">
                        <div :class="{active: popUp.checkBox.isActive}"></div>
                    </div>
                    <span>I’m agree with privacy policy</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                popUp: {
                    isVisible: false,
                    checkBox: {
                        isActive: true
                    },
                    alert: {
                        state: '',
                        message: ''
                    },
                    input: {
                        value: ''
                    }

                },
                info: {
                    message: {
                        error: 'You have already subscribed to the newsletter',
                        success: 'You have successfully subscribed to the newsletter'
                    }
                }

            }
        },
        methods: {
            checkBoxChangeState() {
                this.popUp.checkBox.isActive = !this.popUp.checkBox.isActive
            },
            subscribeHandler() {
                if (localStorage.email == this.popUp.input.value) {
                    this.popUp.alert.state = 'error';
                    this.popUp.alert.message = this.info.message.error;
                } else {
                    localStorage.email = this.popUp.input.value;
                    this.popUp.alert.state = 'success';
                    this.popUp.alert.message = this.info.message.success;
                    this.popUp.input.value = '';
                }
            }

        }

    }

</script>

<style>
    *{
        margin: 0;
        padding: 0;
        font-family: 'Roboto', sans-serif;
        color: #2F3639;
        box-sizing: border-box;
    }

    .app{
        height: 100vh;
        width: 100vw;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .main-but{    
        width: 106px;
        height: 40px;
        background: #C24DFE;
        border-radius: 35px;
        border: none;
        font-weight: 700;
        color: white;
    }

    .pop-up{
        position: relative;
        width: 864px;
        height: 502px;
        background: #FFFFFF;
        box-shadow: 0px 8px 20px rgba(68, 75, 77, 0.15);
        border-radius: 8px;
    }

    .img-block{
        position: absolute;
        width: 581px;
        height: 502px;
        left: 283px;
        top: 0px;
        background-image: url('./img/back1.svg');
        background-size: cover;
    }



    .cross-but{
        position: absolute;
        background-image: url('./img/cross.svg');
        background-size: cover;
        width: 10px;
        height: 10px;
        left: 559px;
        top: 12px;
    }

    .percent{
        width: 416px;
        height: 104px;
        font-size: 104px;
        font-weight: 700;
        margin: 30px 0 0 32px;
    }

    .percent>span{
        font-size: 24px;
    }

    .first-order{
        width: 339px;
        height: 112px;
        margin: 16px 0 0 32px;
    }

    .first-order>span{
        color: #828688;
        font-size: 24px;
        font-weight: bold;
    }

    .first-order>hr{
        border: none;
        border-top: 2px solid #C24DFE;
        width: 67px;
        margin: 24px 0 24px 0;
    }

    .first-order>p{
        font-size: 14px;
        color: #595E61;
        width: 373px;
    }

    .email{
        margin: 40px 0 0 32px;
        height: 150px;
    }

    .email>span{
        color: #828688;
        font-size: 12px;
        font-weight: 700;
    }

    .email>input{
        all: unset;
        display: block;
        width: 302px;
        height: 40px;
        border: 1px solid #D5D7D7;
        border-radius: 6px;
        margin-top: 8px;
        font-size: 14px;
        color: #ACAFB0;
        padding-left: 10px;
    }

    .email>button{
        width: 106px;
        height: 40px;
        border-radius: 35px;
        color: white;
        background-color: #C24DFE;
        border: none;
        font-size: 12px;
        font-weight: 700;
        margin: 16px 0 16px 0;
    }
    .i-am-agree{
        display: flex;
        align-items: center;
    }

    .i-am-agree>.checkbox{
        width: 16px;
        height: 16px;
        border: 2px solid #C24DFE;
        border-radius: 4px;
        margin-right: 8px;
    }

    .i-am-agree>.checkbox>div.active{
        height: 8px;
        width: 8px;
        border-radius: 2px;     
        background-color: #C24DFE;
        margin: 2px;
    }

    .i-am-agree>.checkbox>div{
        height: 8px;
        width: 8px;
        border-radius: 2px;     
        background-color: white;
        margin: 2px;
    }

    .i-am-agree>span{
        font-size: 14px;
        color: #595E61;
        font-weight: 500;
    }

    .alert{
        position: absolute;    
        margin: 15px 0 0 32px;
    }

    .alert.success{
        color: green;
    }

    .alert.error{
        color: red;
    }

</style>