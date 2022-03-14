<template>
  <div>
    <div class="top">
      <i class="el-icon-user-solid"></i>
      <span class="title">管理员</span>
    </div>
    <div>
      <el-tabs v-model="activeName" @tab-click="handleClick">
        <el-tab-pane label="用户信息管理" name="first">
          <el-table :data="books" style="width: 90%; margin: 0 auto">
            <el-table-column prop="username" label="用户名" width="100px"> </el-table-column>
            <el-table-column prop="psw" label="密码" width="100px"> </el-table-column>
            <el-table-column prop="uname" label="姓名" width="160px">  </el-table-column>
         
            <el-table-column prop="phonenumber" label="手机号" width="90px"> </el-table-column>
            <el-table-column prop="address" label="收获地址" width="170px">
            </el-table-column>
            <el-table-column prop="headimg" label="头像" width="120px">
            </el-table-column>
            <el-table-column prop="brith" label="生日" width="80px">
            </el-table-column>
       


           
          </el-table>
        </el-tab-pane>

        <el-tab-pane label="图书信息管理" name="second">
          <span class="tianjia"
            ><el-button type="primary" @click="BookDialogFormVisible = true"
              >添加</el-button
            ></span
          >
          <el-table :data="books" style="width: 90%; margin: 0 auto">
            <el-table-column label="商品" width="100px">
              <template slot-scope="scope">
                <img :src="scope.row.img" alt="图片打开失败" />
              </template>
            </el-table-column>
            <el-table-column prop="bookname" label="书名" width="160px">
            </el-table-column>
            <el-table-column label="类型" width="60px">
              <template slot-scope="scope">
                <div>
                  {{
                    scope.row.booktype == "1"
                      ? "小说"
                      : scope.row.booktype == "2"
                      ? "文学"
                      : scope.row.booktype == "3"
                      ? "科技"
                      : scope.row.booktype == "4"
                      ? "杂志"
                      : scope.row.booktype == "5"
                      ? "漫画"
                      : "外文书刊"
                  }}
                </div>
              </template>
            </el-table-column>
            <el-table-column label="卖点" width="270px">
              <template slot-scope="scope">
                <div class="sellpoint">
                  {{ scope.row.sellpoint }}
                </div>
              </template>
            </el-table-column>
            <el-table-column prop="price" label="价格(元/本)" width="70px">
            </el-table-column>
            <el-table-column prop="num" label="库存" width="70px">
            </el-table-column>
            <el-table-column prop="author" label="作者" width="80px">
            </el-table-column>
            <el-table-column label="热推" width="70px">
              <template slot-scope="scope">
                <div>
                  {{ scope.row.hot == "1" ? "热" : "否" }}
                </div>
              </template>
            </el-table-column>
            <el-table-column label="最新" width="70px">
              <template slot-scope="scope">
                <div>
                  {{ scope.row.newly == "1" ? "新" : "否" }}
                </div>
              </template>
            </el-table-column>
            <el-table-column label="操作">
              <template slot-scope="scope">
              <el-button type="success" @click="revise(scope.row)">修改</el-button>
              <el-button type="danger" @click="del(scope.row )">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-tab-pane>
        <el-tab-pane label="订单管理" name="third">
          <el-table :data="books" style="width: 90%; margin: 0 auto">
            <el-table-column label="商品" width="100px">
              <template slot-scope="scope">
                <img :src="scope.row.img" alt="图片打开失败" />
              </template>
            </el-table-column>
            <el-table-column prop="orderid" label="订单编号" width="160px">
            </el-table-column>
           <el-table-column prop="username" label="用户名" width="80px"></el-table-column>
            <el-table-column prop="consignee" label="收货人" width="90px">
              
            </el-table-column>
            <el-table-column prop="address" label="收获地址" width="170px">
            </el-table-column>
            <el-table-column prop="tel" label="手机号" width="120px">
            </el-table-column>
            <el-table-column prop="sumprice" label="金额" width="80px">
            </el-table-column>
       


            <el-table-column  label="是否收获" width="160px">
              <template slot-scope="scope">
                <div>
                  {{scope.row.receipt=='0'? '未收货' : '已收货'}}
                </div>

              </template>
            </el-table-column>
            <el-table-column prop="receivingtime" label="下单时间" width="160px">
            </el-table-column>
            <el-table-column prop="detail" label="详情" width="160px">
            </el-table-column>
            <el-table-column label="操作">
              <template slot-scope="scope">
              <el-button type="success" @click="revise(scope.row)">修改</el-button>
              <!-- <el-button type="danger" @click="del(scope.row )">删除</el-button> -->
              </template>
            </el-table-column>
          </el-table>
        </el-tab-pane>
      </el-tabs>
    </div>
    <!--  -->

    <el-dialog title="图书信息" :visible.sync="BookDialogFormVisible">
      <el-form v-model="addbook">
        <el-form-item label="图书名称:" :label-width="formLabelWidth">
          <el-input v-model="addbook.bookname" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="图书类型:" :label-width="formLabelWidth">
          <el-radio-group v-model="addbook.booktype">
            <el-radio label="1">小说</el-radio>
            <el-radio label="2">文学</el-radio>
            <el-radio label="3">科技</el-radio>
            <br /><br />
            <el-radio label="4">杂志</el-radio>
            <el-radio label="5">漫画</el-radio>
            <el-radio label="6">外文书刊</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="卖点:" :label-width="formLabelWidth">
          <el-input
            type="textarea"
            v-model="addbook.sellpoint"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item label="价格（元/本）:" :label-width="formLabelWidth">
          <el-input v-model="addbook.price" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="作者:" :label-width="formLabelWidth">
          <el-input v-model="addbook.author" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="数量:" :label-width="formLabelWidth">
          <el-input
            v-model="addbook.num"
            autocomplete="off"
            type="number"
          ></el-input>
        </el-form-item>
        <el-form-item label="热推:" :label-width="formLabelWidth">
          <el-radio-group v-model="addbook.hot">
            <el-radio label="1">是</el-radio>
            <el-radio label="0">否</el-radio>
          </el-radio-group>
        </el-form-item>

        <el-form-item label="最新:" :label-width="formLabelWidth">
          <el-radio-group v-model="addbook.newly">
            <el-radio label="1">是</el-radio>
            <el-radio label="0">否</el-radio>
          </el-radio-group>
        </el-form-item>

        <el-form-item label="上传图片:" :label-width="formLabelWidth" prop="logoUrl">
          <input
              type="file"
              accept="image/*"
              @change="changeImage()"
              ref="avatarInput"
              style="display:none"
            />
            <div class="pic_list_box" @click="upLoad">
              <div class="pic_list" v-show="imgDatas.length">
                <div v-for="(src,index) in imgDatas" :key="index">
                  <el-image
                    style="width: 100px; height: 100px"
                    :src="src"
                    :preview-src-list="imgDatas">
                  </el-image>
                </div>
              </div>
              <i  v-show="!imgDatas.length" class="el-icon-plus avatar-uploader-icon"  ></i>
            </div>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="BookCancel">重置</el-button>
        <el-button type="primary" @click="submit">确 定</el-button>
      </div>
    </el-dialog>

    <el-dialog title="修改" :visible.sync="reviseDialog">
      <el-form v-model="listData">
        <el-form-item label="价格（元/本）:" :label-width="formLabelWidth">
          <el-input v-model="listData.price" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="数量:" :label-width="formLabelWidth">
          <el-input
            v-model="listData.num"
            autocomplete="off"
            type="number"
          ></el-input>
        </el-form-item>
        <el-form-item label="卖点:" :label-width="formLabelWidth">
          <el-input
            type="textarea"
            v-model="listData.sellpoint"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item label="热推:" :label-width="formLabelWidth">
          <el-radio-group v-model="listData.hot">
            <el-radio :label="1">是</el-radio>
            <el-radio :label="0">否</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="最新:" :label-width="formLabelWidth">
          <el-radio-group v-model="listData.newly">
            <el-radio :label="1">是</el-radio>
            <el-radio :label="0">否</el-radio>
          </el-radio-group>
        </el-form-item>


      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="reviseDialog=false">取消</el-button>
        <el-button type="primary" @click="submitRevise">确 定</el-button>
      </div>
    </el-dialog>







    <div class="ft">
      <div class="text">版权所有 © 1996-2021，亚马逊公司或其关联公司</div>
      <div class="text">互联网药品信息服务资格证书 (京)-非经营性-2012-0005</div>
      <div class="text">
        京公网安备11010502030232号增值电信业务经营许可证：合字
        B2-20090004营业执照：91110000717883277U
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      reviseDialog:false,
      // listData
      imgDatas:[],
      img:"",
      activeName: "second",
      books: [],
      BookDialogFormVisible: false,
      addbook: {
        bookname: "",
        booktype: "",
        sellpoint: "",
        price: "",
        author: "",
        hot: "",
        newly: "1",
        num: "",
      },
      formLabelWidth: "120px",
      listData:{
        bookname:'',
        price:'',
        hot:'0'
      }
    };
  },
  mounted() {
    this.$axios.post("http://localhost:8888/book/getall").then((result) => {
      this.books = result.data;
    });
  },
  methods: {
    changeImage() {
      var files = this.$refs.avatarInput.files;
    this.readAndPreview(files)
      this.readAndPreview(files[0])
      if (files.length === 0) {
        return;
      }
    },
    // xiugai 
    revise(row){
   
      this.listData=row
      this.reviseDialog=true
      // this.reviseDialogVisible=true
      console.log(111111,this.listData)
    },

    submitRevise(){
      let params={
        bookname:this.listData.bookname,
        price:this.listData.price,
        num:this.listData.num,
        sellpoint:this.listData.sellpoint,
        hot:this.listData.hot,
        newly:this.listData.newly 
      }
      this.$axios.post('http://localhost:8888/book/update',params).then(res=>{
         if(res.data==1){
            this.$message.success("修改成功");
            this.reviseDialog=false

         }else{
            this.$message.error("修改失败");
         }
      })
    },
    readAndPreview(file) {  
      let that=this  
        console.log('上传',file.name )   
          that.img = "/static/" + file.name; 
        if (/\.(jpe?g|png|gif)$/i.test(file.name)) {
          var reader = new FileReader();
          reader.onload = function(e) {
            // 防止重复上传
            if (that.imgDatas.indexOf(e.target.result) === -1) {
              that.imgDatas.push(e.target.result);
            }
          };
          reader.readAsDataURL(file);
        }
      },
    setUploadFile(file) {
      this.formData = new FormData()
      this.formData.append('files', file, file.name) // 添加到请求体
      this.$http
        .post('/api/dxbase/upload?resType=EVENT', this.formData)
        .then(res=> {
          console.log(res);
        })
    },
    upLoad() {
      // 触发上传图片按钮
      this.$refs.avatarInput.dispatchEvent(new MouseEvent("click"));
    },
    handleClick(tab, event) {
      console.log(tab, event);
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
      
    submit() {
      console.log(this.addbook);
      this.BookDialogFormVisible = false;
      let params = {
        bookname: this.addbook.bookname,
        booktype: this.addbook.booktype,
        sellpoint: this.addbook.sellpoint,
        price: this.addbook.price,
        author: this.addbook.author,
        hot: this.addbook.hot,
        newly: this.addbook.newly,
        num: this.addbook.num,
        img:this.img
      };
      console.log("参数", params);
      this.$axios
        .post("http://localhost:8888/book/add", params)
        .then((result) => {
          if (result.data == 1) {
            this.$message.success("添加成功");
            this.$axios
              .post("http://localhost:8888/book/getall")
              .then((result) => {
                this.books = result.data;
              });
          } else if(result.data == 2){
            this.$message.error("该商品已存在");
          }else{
            this.$message.error("缺少信息");
          }
        });
    },
    BookCancel() {
      this.addbook = {};
    },
    del(row){
       let params = {
        bookname: row.bookname
      };
       this.$axios
        .post("http://localhost:8888/book/del", params)
        .then((result) => {
            if(result.data==1){
              this.$message.success("删除成功");
               this.$axios
              .post("http://localhost:8888/book/getall")
              .then((result) => {
                this.books = result.data;
              });
            }else{
               this.$message.error("删除失败");}
        })
    },
    handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      }
  },
};
</script>
<style  scoped>
.top {
  height: 60px;
  margin-left: 0 !important;
  margin-right: 0 !important;
  background: rgba(117, 47, 147);
  line-height: 60px;
}
.top .title {
  vertical-align: super;
  color: seashell;
  font-family: "微软雅黑";
  font-size: 20px;
}
.top i {
  color: seashell;
  font-size: 40px;
  margin-left: 10px;
}
.ft {
  position: fixed;
  bottom: 0px;
  padding: 10px 0;
  width: 100%;
  background: rgba(117, 47, 147, 0.9);
  bottom: 0px;
}
.ft .text {
  text-align: center;
  width: 100%;
  color: cornsilk;
  font-size: 5px;
  margin: 0px auto;
  line-height: 20px;
}
.tianjia {
  margin-left: 50px;
}
img {
  width: 60px;
  height: 60px;
}
.sellpoint {
  font-size: 7px;
  color: gray;
}
/* 上传图片 */
.pic_list_box{
  /* background: red; */
  border: 1px solid #999;
    width: 100px;
    height: 100px;
    text-align: center;
    line-height: 100px;
}
</style>