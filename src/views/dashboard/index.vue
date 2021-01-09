<template>
  <div class="dashboard-container">
    <!-- 表单验证 -->
    <div class="table">
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-width="100px"
        class="demo-ruleForm"
        style="width: 840px"
      >
        <el-form-item label="游戏名称" prop="gameName">
          <el-input v-model="ruleForm.gameName"></el-input>
        </el-form-item>
        <el-form-item label="游戏类型" prop="type">
          <el-checkbox-group v-model="ruleForm.type" class="el-checkbox-group">
            <el-checkbox label="策略游戏" name="type"></el-checkbox>
            <el-checkbox label="换装游戏" name="type"></el-checkbox>
            <el-checkbox label="射击游戏" name="type"></el-checkbox>
            <el-checkbox label="篮球游戏" name="type"></el-checkbox>
            <el-checkbox label="其他游戏" name="type"></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-form-item label="游戏简介" prop="gameDesc">
          <el-input type="textarea" v-model="ruleForm.gameDesc"></el-input>
        </el-form-item>
        <el-form-item label="游戏操作" prop="gameOperation">
          <el-input type="textarea" v-model="ruleForm.gameOperation"></el-input>
        </el-form-item>
        <el-form-item label="游戏图片" prop="gameImg" v-model="ruleForm.gameImg">
          <el-upload
            action="https://jsonplaceholder.typicode.com/posts/"
            list-type="picture-card"
            :on-preview="handlePictureCardPreview"
            :on-remove="handleRemove"
            class="gameUpload"
            v-model="ruleForm.gameImg"
          >
            <i class="el-icon-plus"></i>
          </el-upload>
          <el-dialog :visible.sync="dialogVisible" v-model="ruleForm.gameImg">
            <img width="100%" :src="dialogImageUrl" alt="" />
          </el-dialog>
        </el-form-item>
        <el-form-item label="游戏上传" prop="gameUpload">
          <el-upload
            action="https://jsonplaceholder.typicode.com/posts/"
            list-type="picture-card"
            :on-preview="handlePictureCardPreview"
            :on-remove="handleRemove"
            class="gameUpload"
          >
            <i class="el-icon-plus"></i>
          </el-upload>
          <el-dialog :visible.sync="dialogVisible">
            <img width="100%" :src="dialogImageUrl" alt="" />
          </el-dialog>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')"
            >立即上传</el-button
          >
          <el-button @click="resetForm('ruleForm')">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
// import { mapGetters } from 'vuex'

export default {
  data() {
    return {
      // 上传
      dialogImageUrl: "",
      dialogVisible: false,
      // 表单
      ruleForm: {
        name: "",
        region: "",
        date1: "",
        date2: "",
        delivery: false,
        type: [],
        resource: "",
        desc: "",
      },
      rules: {
        gameName: [
          { required: true, message: "请输入游戏名称", trigger: "blur" },
          { min: 1, max: 100, message: "长度在 1 到 100 个字符", trigger: "blur" },
        ],
        type: [
          {
            type: "array",
            required: true,
            message: "请至少选择一个游戏类型",
            trigger: "change",
          },
        ],
        resource: [
          { required: true, message: "请选择活动资源", trigger: "change" },
        ],
        gameDesc: [{ required: true, message: "请填写游戏的简介", trigger: "blur" }],
        gameOperation: [{required: true,message: '请填写游戏的操作',trigger: 'blur'}],
        gameImg: [{required: true, message: "请上传游戏图片", trigger: "blur"}],
        gameUpload: [{required: true, message: "请上传游戏", trigger: "blur"}]
      },
    };
  },
  methods: {
    // 上传
    handleRemove(file, fileList) {
      console.log(file, fileList);
    },
    handlePictureCardPreview(file) {
      this.dialogImageUrl = file.url;
      this.dialogVisible = true;
    },
    // 表单
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  },
};
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    .gameUpload {
    display: flex;
    justify-content: center;
  }
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
