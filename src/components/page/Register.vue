<template>
    <div class="login-wrap">
        <div class="ms-login">
            <div class="ms-title">
                <span>注册</span>
            </div>
            <el-form ref="form" :rules="rules" :model="form" label-width="80px">
                <div style="width:100%;display:flex;">
                    <div class="left" style="flex:1">
                        <el-form-item label="真实姓名">
                            <el-input v-model="form.realName"></el-input>
                        </el-form-item>
                        <el-form-item label="用户名">
                            <el-input v-model="form.userName"></el-input>
                        </el-form-item>
                        <el-form-item label="密码">
                            <el-input v-model="form.usePwd"></el-input>
                        </el-form-item>
                        <el-form-item label="性别">
                            <el-radio-group v-model="form.sex">
                                <el-radio label="男"></el-radio>
                                <el-radio label="女"></el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item label="学号">
                            <el-input v-model="form.userId"></el-input>
                        </el-form-item>
                        <el-form-item label="出生日期">
                            <el-col :span="11">
                                <el-date-picker
                                    type="date"
                                    placeholder="出生日期"
                                    value-format="yyyy-MM-dd"
                                    v-model="form.birth"
                                ></el-date-picker>
                            </el-col>
                        </el-form-item>
                        <el-form-item label="地址">
                            <el-cascader @change="selectPlace" :options="options"></el-cascader>
                        </el-form-item>
                    </div>
                    <div class="left" style="flex:1">
                        <el-form-item label="邮箱地址">
                            <el-input v-model="form.email"></el-input>
                        </el-form-item>
                        <el-form-item label="电话号码">
                            <el-input v-model="form.phone"></el-input>
                        </el-form-item>
                        <el-form-item label="身份证">
                            <el-input v-model="form.idCard"></el-input>
                        </el-form-item>
                        <el-form-item label="所属班级">
                            <el-select @change="classChange" v-model="form.classId" placeholder="请选择">
                              <el-option v-for="item in classList" :key="item.classId" :label="item.className" :value="item.classId"></el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="所属部门">
                            <el-select @change="departmentChange" v-model="form.departmentId" placeholder="请选择">
                                <el-option v-for="item in departmentList" :key="item.departmentId" :label="item.departmentName" :value="item.departmentId"></el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="创建时间">
                            <el-col :span="11">
                                <el-date-picker
                                    type="date"
                                    placeholder="创建时间"
                                    value-format="yyyy-MM-dd"
                                    v-model="form.createTime"
                                ></el-date-picker>
                            </el-col>
                        </el-form-item>
                        <el-form-item label="修改时间">
                            <el-col :span="11">
                                <el-date-picker
                                    type="date"
                                    placeholder="修改时间"
                                    value-format="yyyy-MM-dd"
                                    v-model="form.updateTime"
                                ></el-date-picker>
                            </el-col>
                        </el-form-item>
                        <el-form-item>
                            <el-button type="primary" @click="submitForm('form')">注册</el-button>
                            <el-button>取消</el-button>
                            <el-button @click="toLogin">返回登录</el-button>
                        </el-form-item>
                    </div>
                </div>
            </el-form>
        </div>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            classList:[{
              classId:'1',
              className:'一班'
            },{
              classId:'2',
              className:'二班'
            },{
              classId:'3',
              className:'三班'
            }],//班级信息
            departmentList:[{
              departmentId:'1',
              departmentName:'文学社'
            },{
              departmentId:'2',
              departmentName:'学生会'
            },{
              departmentId:'3',
              departmentName:'自律会'
            }],
            form: {
                realName: '', //真实姓名
                userName: '', //用户名
                sex: '男', //性别
                userId: '', //学号
                usePwd: '', //密码
                birth: '', //出生日期
                address: '', //地址
                email: '', //邮箱地址
                idCard: '', //身份证
                phone: '', //电话号码
                createTime: '', //创建时间
                updateTime: '', //修改时间
                classId: '', //所属班级
                className: '', //所属班级名称
                departmentId: '', //所属部门
                departmentName: '' //所属部门名称
            },
            options: [
                {
                    value: '广东省',
                    label: '广东省',
                    children: [
                        {
                            value: '广州市',
                            label: '广州市',
                            children: [
                                {
                                    value: '天河区',
                                    label: '天河区'
                                },
                                {
                                    value: '海珠区',
                                    label: '海珠区'
                                }
                            ]
                        },
                        {
                            value: '东莞市',
                            label: '东莞市',
                            children: [
                                {
                                    value: '长安镇',
                                    label: '长安镇'
                                },
                                {
                                    value: '虎门镇',
                                    label: '虎门镇'
                                }
                            ]
                        }
                    ]
                },
                {
                    value: '湖南省',
                    label: '湖南省',
                    children: [
                        {
                            value: '长沙市',
                            label: '长沙市',
                            children: [
                                {
                                    value: '岳麓区',
                                    label: '岳麓区'
                                }
                            ]
                        }
                    ]
                }
            ],
            rules: {
                realName: [{ required: true, message: '请输入真实姓名', trigger: 'blur' }],
                userName: [{ required: true, message: '请输入用户名', trigger: 'blur' }],
                usePwd: [{ required: true, message: '请选择密码', trigger: 'blur' }],
                sex: [{ required: true, message: '请选择性别', trigger: 'change' }],
                usePwd: [{ required: true, message: '请选择密码', trigger: 'blur' }],
                password: [{ required: true, message: '请输入密码', trigger: 'blur' }],
                userId: [{ required: true, message: '请输入学号', trigger: 'blur' }],
                birth: [{ required: true, message: '请选择出生日期', trigger: 'change' }],
                address: [{ required: true, message: '请输入地址', trigger: 'blur' }],
                email: [{ required: true, message: '请输入邮箱地址', trigger: 'blur' }],
                idCard: [{ required: true, message: '请输入身份证号', trigger: 'blur' }],
                phone: [{ required: true, message: '请输入电话号码', trigger: 'blur' }],
                classId: [{ required: true, message: '请选择所属班级', trigger: 'change' }],
                className: [{ required: true, message: '请输入班级名称', trigger: 'blur' }],
                departmentId: [{ required: true, message: '请选择所属部门', trigger: 'change' }],
                departmentName: [{ required: true, message: '请输入部门名称', trigger: 'blur' }],
                createTime: [{ required: true, message: '请输入创建时间', trigger: 'blur' }],
                updateTime: [{ required: true, message: '请输入修改时间', trigger: 'blur' }]
            }
        };
    },
    methods: {
        submitForm(form) {
          const {model} = this.$refs[form]
          console.log(model);
          this.$axios.post(`${this.$baseUrl}user/register.do`,{
            realName:model.realName,
            userName:model.userName,
            usePwd:model.usePwd,
            sex:model.sex,
            usePwd:model.usePwd,
            password:model.password,
            userId:model.userId,
            birth:model.birth,
            address:model.address,
            email:model.email,
            idCard:model.idCard,
            phone:model.phone,
            classId:model.classId,
            className:model.className,
            departmentId:model.departmentId,
            departmentName:model.departmentName,
            createTime:model.createTime,
            updateTime:model.updateTime,
          }).then(res=>{
            console.log(res);
          })
            /* this.$refs[form].validate(valid => {
                if (valid) {
                    this.$message.success('注册成功');
                    setTimeout(() => {
                        this.$router.push('/login');
                    }, 1000);
                } else {
                    console.log('error submit!!');
                    return false;
                }
            }); */
        },
        toLogin() {
            this.$router.push('/login');
        },
        selectPlace(value){
          this.form.address = value[0] + value[1] + value[2]
          console.log(this.form.address);
        },
        classChange(value){
          this.classList.map(item=>{
            if(value == item.classId){
              this.form.className = item.className
            }
          })
        },
        departmentChange(value){
          this.departmentList.map(item=>{
            if(value == item.departmentId){
              this.form.departmentName = item.departmentName
            }
          })
        }
    }
};
</script>

<style scoped>
.el-input {
    width: 220px;
}
.ms-login {
    width: 700px;
}
.login-wrap {
    position: relative;
    width: 100%;
    height: 100%;
    background-image: url(../../assets/img/login-bg.jpg);
    background-size: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.ms-title {
    width: 100%;
    line-height: 50px;
    text-align: center;
    font-size: 20px;
    color: #000;
    border-bottom: 1px solid #ddd;
    position: relative;
}
.ms-login {
    position: absolute;
    width: 700px;
    border-radius: 5px;
    background: rgba(255, 255, 255, 0.3);
    overflow: hidden;
    padding: 0 20px;
}
.el-form {
    margin-top: 20px;
}
.ms-content {
    padding: 30px 30px;
}
.login-btn {
    text-align: center;
}
.login-btn button {
    width: 100%;
    height: 36px;
    margin-bottom: 10px;
}
.login-tips {
    font-size: 12px;
    line-height: 30px;
    color: #fff;
    cursor: pointer;
}
</style>