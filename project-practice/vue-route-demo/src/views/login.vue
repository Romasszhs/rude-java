<template>
    <div>
        <p>用户名：<input type='text' v-model="userName"></p>
        <p>密码：<input type='text' v-model="passWord"></p>
        <button @click="login()">登录</button>
    </div>
</template>

<script>



    //import axios from "axios";
    //axios.defaults.withCredentials = false

    import { mapMutations } from 'vuex';




    export default {
        name: "login",
        data(){
            return{
                userName:'admin',
                passWord:'123'
            }
        },
        methods:{
          ...mapMutations(['storeLogin']),
            login(){

                this.$axios({
                    url:'http://localhost:9091/auth/login',
                    method:"post",
                    data:{"username":this.userName, "password":this.passWord},
                    headers:{
                        "Content-Type": "application/json"
                    }
                }).then(res =>{
                  if (res.data.code==="200"){
                    this.storeLogin({token:res.data.result})
                    console.log(res)
                    console.log(res.data.result)
                    this.$router.push('/index')
                  }else {

                    alert("登录失败,请输入正确信息")
                  }
                })

            }
        }
    }
</script>

<style scoped>

</style>