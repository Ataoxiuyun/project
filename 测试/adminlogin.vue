<template>
  <div>
   
    <div class="bg" :style="{ height: height }">
      <div class="login">
        <h2>管理员登录</h2>

        <el-form ref="form" label-width="80px">
           
          <el-form-item label="管理员">
            <el-input v-model="adminname" type="text"></el-input>
          </el-form-item>
          <el-form-item label="密码">
            <el-input v-model="psw" type="password"></el-input>
          </el-form-item>
          <el-form-item class="ria">
           
            <el-button type="primary" @click="onSubmit">登录</el-button>
            <el-button @click="cancel">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name:'',
      adminname: "",
      psw: "",
      height: "",
      inHeight: "",
       imgList: [],
        size: 0,
           imgDatas: []
    };
  },
  mounted() {
    this.height = window.screen.height - 105 + "px";
  },
  methods: {
    onSubmit() {
       let params={
        adminname:this.adminname,
        psw:this.psw
      }
       this.$axios.post('http://localhost:8888/admin',params).then(result=>{
          if(result.data==1){
             this.$message.success('登录成功');
              this.$router.push({path:'/admin'})
          }else if(result.data==3){
              this.$message.error('账号不存在');
          }else{
               this.$message.error('密码错误');
          }
      })
    },
    cancel(){
      // this.formData=''
      this.adminname=''
      this.psw=''
      // console.log(11,this.formData)
    }
  },
};
</script>
<style scoped>
.bg {
  width: 100%;
  background: rgba(117, 47, 147);
  padding-top:1px ;
}

.login {
  width: 30%;
  height: 300px;
  margin-left: 35%;
  margin-top: 100px;
  background-color: white;
  padding: 20px;
  border-radius: 5px;
}
.login h2 {
  text-align: center;
  margin-top: 20px;
  margin-bottom: 40px;
}
.ria{
    margin-left: 120px;
    margin-top: 40px;
}



   
</style>