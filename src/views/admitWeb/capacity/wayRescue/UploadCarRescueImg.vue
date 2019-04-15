<template>
    <div>
        <!--上传证件弹窗-->
        <el-dialog class="capacity-pop upload_pop capacity-pop-big capacity-line" title="上传车辆证件" :visible.sync="visible" width="650px" center
                   :before-close="closeUploadCarResImgRescue">
            <div class="capacity-pop-in">

                <el-form :model="uploadPapersForm" :rules="uploadPapersRules" ref="uploadPapersForm" class="demo-ruleForm papers-item">
                    <el-form-item class="upload_box">
                        <span class="tit_tit"><i class="not-null">*</i>行驶证首页</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="driving_license_front"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.driving_license_front_imageUrl"
                                 :src="uploadPapersForm.driving_license_front_imageUrl"
                                 :imageType="uploadPapersForm.driving_license_front_imageUrl_type"
                                 :imgName="uploadPapersForm.driving_license_front_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '1'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box">
                        <span class="tit_tit"><i class="not-null">*</i>行驶证副页</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="driving_license_second"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.driving_license_second_imageUrl"
                                 :src="uploadPapersForm.driving_license_second_imageUrl"
                                 :imageType="uploadPapersForm.driving_license_second_imageUrl_type"
                                 :imgName="uploadPapersForm.driving_license_second_imageUrl_name"
                                 class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '1'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box">
                        <span class="tit_tit"><i class="not-null">*</i>行驶证背面</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="driving_license_back"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.driving_license_back_imageUrl"
                                 :src="uploadPapersForm.driving_license_back_imageUrl"
                                 :imageType="uploadPapersForm.driving_license_back_imageUrl_type"
                                 :imgName="uploadPapersForm.driving_license_back_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '2'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box">
                        <span class="tit_tit">机动车登记证书</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="car_reg_cert"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.car_reg_cert_imageUrl"
                                 :src="uploadPapersForm.car_reg_cert_imageUrl"
                                 :imageType="uploadPapersForm.car_reg_cert_imageUrl_type"
                                 :imgName="uploadPapersForm.car_reg_cert_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '5'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box">
                        <span class="tit_tit">道路运输证</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="car_reg_cert"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.car_reg_cert_imageUrl"
                                 :src="uploadPapersForm.car_reg_cert_imageUrl"
                                 :imageType="uploadPapersForm.car_reg_cert_imageUrl_type"
                                 :imgName="uploadPapersForm.car_reg_cert_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '4'">查看示例</div>
                    </el-form-item>

                    <el-form-item class="upload_box">
                        <span class="tit_tit"><i class="not-null">*</i>交强险保单</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="traffic_insurance"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.traffic_insurance_imageUrl"
                                 :src="uploadPapersForm.traffic_insurance_imageUrl"
                                 :imageType="uploadPapersForm.traffic_insurance_imageUrl_type"
                                 :imgName="uploadPapersForm.traffic_insurance_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg">&nbsp;</div>
                    </el-form-item>
                    <el-form-item class="upload_box">
                        <span class="tit_tit"><i class="not-null">*</i>商业车险保单</span>
                        <el-upload
                                class="avatar-uploader"
                                name="commercial_insurance"
                                :action="action"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <!--图片验证 :before-upload="common.beforeAvatarUpload" -->
                            <img v-if="uploadPapersForm.commercial_insurance_imageUrl"
                                 :src="uploadPapersForm.commercial_insurance_imageUrl"
                                 :imageType="uploadPapersForm.commercial_insurance_imageUrl_type"
                                 :imgName="uploadPapersForm.commercial_insurance_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg">&nbsp;</div>
                    </el-form-item>
                    <el-form-item class="upload_box">
                        <span class="tit_tit"><i class="not-null">*</i>车辆正面45°照片</span>
                        <el-upload
                                class="avatar-uploader"
                                :action="action"
                                name="car_front_45"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="updateSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="uploadPapersForm.car_front_45_imageUrl"
                                 :src="uploadPapersForm.car_front_45_imageUrl"
                                 :imageType="uploadPapersForm.car_front_45_imageUrl_type"
                                 :imgName="uploadPapersForm.car_front_45_imageUrl_name" class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" style="position: relative;left: -10px;" @click="sampleImg = true,sampleType = '3'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="papers-sm">
                        <h2>上述证件要求</h2>
                        <ul>
                            <li>1、上述证件中所有信息清晰可见，字迹无PS、遮挡、涂改、模糊等情况</li>
                            <li>2、证件必须完整，证件四个边角需漏出，证件无残缺、断裂、破损等情况</li>
                            <li>3、必须为清晰、完整的彩色原件扫描件或数码照</li>
                            <li>4、支持上传图片格式-jpg/png/bmp,图片大小在3M以内</li>
                        </ul>
                    </el-form-item>
                    <div class="import-bottom">
                        <el-button @click="closeUploadCarResImgRescue">取 消</el-button>
                        <el-button type="primary" @click="next">下一步</el-button>
                    </div>

                </el-form>
            </div>
        </el-dialog>

        <!--核对并完善信息弹窗-->
        <el-dialog class="capacity-pop capacity-line capacity-pop-big" title="核对并完善信息" :visible.sync="checkInfo" width="64%" center>
            <div class="capacity-pop-in">
                <p class="checkInfo-tip">已为您自动识别部分信息，请仔细核对并完善</p>
                <el-form :model="checkInfoForm2" :rules="checkInfoRules2" ref="checkInfoForm2" label-width="122px" class="demo-ruleForm">
                    <div class="info-item clear">
                        <el-form-item label="车牌号码" prop="dlPlateNo">
                            <el-input v-model="checkInfoForm2.dlPlateNo"></el-input>
                        </el-form-item>
                        <el-form-item label="车牌类型" prop="dlPlateType">
                            <el-select v-model="checkInfoForm2.dlPlateType" placeholder="请选择">
                                <el-option value=1 label="黄牌"></el-option>
                                <el-option value=2 label="蓝牌"></el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="所有人" prop="dlBelongUser">
                            <el-input v-model="checkInfoForm2.dlBelongUser"></el-input>
                        </el-form-item>
                        <el-form-item label="使用性质" prop="dlUseNature">
                            <el-select v-model="checkInfoForm2.dlUseNature" placeholder="请选择">
                                <el-option value=1 label="货运"></el-option>
                                <el-option value=2 label="营运"></el-option>
                                <el-option value=3 label="非营运"></el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="车辆类型" prop="dlCarType">
                            <el-input v-model="checkInfoForm2.dlCarType"></el-input>
                        </el-form-item>
                        <el-form-item label="车架号" prop="dlCarVin">
                            <el-input v-model="checkInfoForm2.dlCarVin"></el-input>
                        </el-form-item>
                        <el-form-item label="品牌型号" prop="dlBrand">
                            <el-input v-model="checkInfoForm2.dlBrand"></el-input>
                        </el-form-item>
                        <el-form-item label="注册日期" prop="dlRegisterTime">
                            <el-date-picker
                                    v-model="checkInfoForm2.dlRegisterTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="发动机号码" prop="dlEngineNo">
                            <el-input v-model="checkInfoForm2.dlEngineNo"></el-input>
                        </el-form-item>
                        <el-form-item label="整备质量" prop="dlHostlingWeight">
                            <el-input v-model="checkInfoForm2.dlHostlingWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="发证日期" prop="dlIssueTime">
                            <el-date-picker
                                    v-model="checkInfoForm2.dlIssueTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="准牵引质量" prop="dlTractionWeight">
                            <el-input v-model="checkInfoForm2.dlTractionWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="核定载质量" prop="dlLoadWeight">
                            <el-input v-model="checkInfoForm2.dlLoadWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="外廓尺寸" prop="dlGabarite">
                            <el-input v-model="checkInfoForm2.dlGabarite"></el-input>
                        </el-form-item>
                        <el-form-item label="强制报废日期止" prop="dlScrapEndTime">
                            <el-date-picker
                                    v-model="checkInfoForm2.dlScrapEndTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="检验有效期止" prop="dlCheckEndTime">
                            <el-date-picker
                                    v-model="checkInfoForm2.dlCheckEndTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                    </div>
                </el-form>
                <div class="import-bottom">
                    <el-button @click="checkInfo = false">上一步</el-button>
                    <el-button type="primary" @click="submitCheckInfoForm2">确 定</el-button>
                </div>
            </div>
        </el-dialog>

    </div>
</template>

<script>
    import SampleGraph from '../../SampleGraph'  //示例图
    export default {
        name: "UploadCarRescueImg",
        inject:["reload"],
        components:{
            'SampleGraph':SampleGraph
        },
        data(){

            return {
                sampleImg: false,
                sampleType:'',
                action: this.common.CONSTANT.UPLOADIMGPATH + 'recognizeImage',
                imgObjectList:[],  //图片缓存
                companyId:'',

                uploadPapersForm:{
                    pkId:'',
                    car_front_45_imageUrl: '',   //车辆前45度
                    car_front_45_imageUrl_type: '',
                    car_front_45_imageUrl_name: '',
                    driving_license_front_imageUrl: '',   //行驶证首页
                    driving_license_front_imageUrl_type: '',
                    driving_license_front_imageUrl_name: '',
                    driving_license_second_imageUrl: '',   //行驶证副页
                    driving_license_second_imageUrl_type: '',
                    driving_license_second_imageUrl_name: '',
                    driving_license_back_imageUrl: '',   //行驶证背页
                    driving_license_back_imageUrl_type: '',
                    driving_license_back_imageUrl_name: '',
                    car_reg_cert_imageUrl: '', //机动车登记证书
                    car_reg_cert_imageUrl_type: '',
                    car_reg_cert_imageUrl_name: '',
                    traffic_insurance_imageUrl: '', //交强险
                    traffic_insurance_imageUrl_type: '',
                    traffic_insurance_imageUrl_name: '',
                    commercial_insurance_imageUrl: '', //商业险
                    commercial_insurance_imageUrl_type: '',
                    commercial_insurance_imageUrl_name: '',

                },
                uploadPapersRules:{},

                checkInfo:false,  //核对并完善信息弹窗
                checkInfoForm:{
                    dlPlateNo:'',
                    dlPlateType:'',
                    dlBelongUser:'',
                    dlUseNature:'',
                    dlCarType:'',
                    dlCarVin:'',
                    dlBrand:'',
                    dlRegisterTime:'',
                    dlEngineNo:'',
                    dlHostlingWeight:'',
                    dlIssueTime:'',
                    dlTractionWeight:'',
                    dlLoadWeight:'',
                    dlGabarite:'',
                    dlScrapEndTime:'',
                    dlCheckEndTime:''
                },
                checkInfoRules:{
                    dlPlateNo:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlPlateType:{required: true, message: '此项不能为空', trigger: 'change'},
                    dlBelongUser:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlUseNature:{required: true, message: '此项不能为空', trigger: 'change'},
                    dlCarType:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlCarVin:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlBrand:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlRegisterTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                    dlEngineNo:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlHostlingWeight:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlIssueTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                    dlTractionWeight:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlLoadWeight:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlGabarite:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlScrapEndTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                    dlCheckEndTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                },
                checkInfoForm2:{
                    dlPlateNo:'',
                    dlPlateType:'',
                    dlBelongUser:'',
                    dlUseNature:'',
                    dlCarType:'',
                    dlCarVin:'',
                    dlBrand:'',
                    dlRegisterTime:'',
                    dlEngineNo:'',
                    dlHostlingWeight:'',
                    dlIssueTime:'',
                    dlTractionWeight:'',
                    dlLoadWeight:'',
                    dlGabarite:'',
                    dlScrapEndTime:'',
                    dlCheckEndTime:''
                },
                checkInfoRules2:{
                    dlPlateNo:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlPlateType:{required: true, message: '此项不能为空', trigger: 'change'},
                    dlBelongUser:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlUseNature:{required: true, message: '此项不能为空', trigger: 'change'},
                    dlCarType:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlCarVin:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlBrand:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlRegisterTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                    dlEngineNo:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlHostlingWeight:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlIssueTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                    dlTractionWeight:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlLoadWeight:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlGabarite:{required: true, message: '此项不能为空', trigger: 'blur'},
                    dlScrapEndTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                    dlCheckEndTime:{type: 'date',required: true, message: '请选择日期', trigger: 'change'},
                }
            }
        },
        props: {
            visible: {
                type: Boolean,
                default: false
            },
            uploadCarRescuePkId: {
                type: String,
                default: ""
            },
            ctaliTypes:{
                default:[]
            }

        },
        created: function () {
            let company = this.common.fetchData("company");
            this.companyId = company['pkId'];
        },
        methods:{
            //添加车辆取消操作
            closeUploadCarResImgRescue() {
                console.log("clear cache..");
                this.checkInfoForm2 = {};
                this.imgObjectList = [];

                let refCheckInfoForm = this.$refs['checkInfoForm2'];
                if (refCheckInfoForm) {
                    console.log("clear checkInfoForm2");
                    refCheckInfoForm.resetFields();
                    refCheckInfoForm.clearValidate();
                }
                this.$emit('update:visible', false);
                this.reload();
            },
            submitCheckInfoForm2(){
                let that = this;
                this.$refs.checkInfoForm2.validate((valid) => {
                    if (valid) {
                        this.checkInfo = false; //关闭弹窗
                        let params = {};
                        var form = that.checkInfoForm2;
                        let company = that.common.fetchData("company");
                        var ltdCarRescue = {};
                        ltdCarRescue.pkId = form.pkId;
                        ltdCarRescue.dlPlateNo = form.dlPlateNo; //车牌号
                        ltdCarRescue.dlPlateType = form.dlPlateType; //车牌类型
                        ltdCarRescue.dlBelongUser = form.dlBelongUser; //所有人
                        ltdCarRescue.dlUseNature = form.dlUseNature; //使用性质
                        ltdCarRescue.dlCarType = form.dlCarType; //车辆类型
                        ltdCarRescue.dlCarVin = form.dlCarVin; //车架号
                        ltdCarRescue.dlBrand = form.dlBrand; //品牌
                        ltdCarRescue.dlRegisterTime = form.dlRegisterTime; //注册时间
                        ltdCarRescue.dlEngineNo = form.dlEngineNo; //发动机号码
                        ltdCarRescue.dlHostlingWeight = form.dlHostlingWeight; // 整备质量
                        ltdCarRescue.dlIssueTime = form.dlIssueTime; //行驶证发证时间
                        ltdCarRescue.dlTractionWeight=form.dlTractionWeight; //准牵引质量
                        ltdCarRescue.dlLoadWeight = form.dlLoadWeight; //核定载质量
                        ltdCarRescue.dlGabarite = form.dlGabarite;//外廓尺寸
                        ltdCarRescue.dlScrapEndTime = form.dlScrapEndTime; //校验有效期
                        ltdCarRescue.dlCheckEndTime = form.dlCheckEndTime; //强制报废期
                        ltdCarRescue.companyId=company['pkId'];
                        params.ltdCarRescue = ltdCarRescue;
                        params.submitType = 2; //2次提交
                        var data = {
                            data: JSON.stringify(params)
                        }
                        that.$post("ltdCarRescue/updateCarInfo", data).then((response) => {
                            var data = response.response;
                            if (response.code == 0) {
                                that.$message.error(response.msg);
                            } else {
                                var errTypes = {2: "车辆信息", 3: "交强险保险单号", 4: "商业险保险单号"};
                                if (data && errTypes[response.code]) {
                                    var errMsg = "当前添加msg已存在，无法需重复添加".replace("msg", errTypes[response.code]);
                                    that.$message.error(errMsg);
                                } else if (response.code == 1) {
                                    that.$message.info(response.msg);
                                    that.reload();
                                    that.$refs['checkInfoForm2'].resetFields();//移除校验结果并重置字段值
                                } else {
                                    that.$message.error(response.msg);
                                }

                            }

                        }).catch(() => {
                            that.$message.error('消息保存失败');
                        });

                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });

            },
            next(){ //下一步操作
                let that = this;
                this.$refs.uploadPapersForm.validate((valid) => {
                    if (valid) {
                        this.$refs['uploadPapersForm'].clearValidate();//清空校验

                        let params = {};
                        let ltdCarRescue = {};
                        ltdCarRescue.companyId = that.companyId;
                        params.submitType = 1; //1次提交
                        ltdCarRescue.pkId=that.uploadPapersForm.pkId;
                        params.ltdCarRescue = ltdCarRescue;
                        let companyImgList = that.getAddCarRescueImgs(that.uploadPapersForm, that.imgObjectList);
                        params.companyImgList = companyImgList;
                        var data = {
                            data: JSON.stringify(params)
                        };
                        //console.log(data);
                        that.$post("ltdCarRescue/updateCarInfo", data).then((response) => {
                            var data = response.response;
                            if (response.code == 0) {
                                that.$message.error(response.msg);
                            } else {
                                 if (response.code == 1) {
                                    var dbRescue = data.ltdCarRescue;
                                    that.uploadPapersForm.pkId = dbRescue.pkId;
                                    that.checkInfoForm2.pkId = dbRescue.pkId;
                                    that.imgObjectList = data.companyImgList;
                                    that.checkInfo = true;
                                } else {
                                    that.$message.error(response.msg);
                                }

                            }
                        }).catch(() => {
                            that.$message.error('消息保存失败');
                        });

                    } else {
                        console.log('valid error submit!!');
                        return false;
                    }
                });

            },
            pottingCheckInfoForm(srcData) {  //填充确认框值
                let checkInfoForm2 = {
                    dlPlateNo :srcData.dlPlateNo, //车牌号
                    dlPlateType :srcData.dlPlateType, //板式
                    dlBelongUser :srcData.dlBelongUser, //所属人
                    dlUseNature :srcData.dlUseNature, //使用性质
                    dlCarType :srcData.dlCarType, //车辆类型
                    dlCarVin :srcData.dlCarVin, //车架号
                    dlBrand :srcData.dlBrand, //品牌
                    dlRegisterTime :srcData.dlRegisterTime, //注册日期
                    dlHostlingWeight :srcData.dlHostlingWeight, //整备质量
                    dlEngineNo :srcData.dlEngineNo, //发动机号码
                    dlIssueTime :srcData.dlIssueTime, //行驶证发证时间
                    dlTractionWeight :srcData.dlTractionWeight, //准牵引质量
                    dlLoadWeight :srcData.dlLoadWeight, //核定载质量
                    dlGabarite :srcData.dlGabarite, //外廓尺寸
                    dlScrapEndTime :srcData.dlScrapEndTime,//强制报废日期止
                    dlCheckEndTime :srcData.dlCheckEndTime //检验有效期止
                }
                this.checkInfoForm2 = checkInfoForm2;
            },
            requestUpload(obj) {
                let that = this;
                obj.companyId = that.companyId;
                this.common.uploadImgFun(obj, this);
            },
            handleAvatarSuccess(res, file) {
                let that = this;
                let data = JSON.parse(res.data);
                //console.log("data-->"+data);
                let imageType = data['resultData']['imageType'];
                let imageTypeValue = data['resultData']['imageTypeValue'];
                let filePath = data['resultData']['filePath'];
                let imageUrl = imageType + "_imageUrl";
                let imageUrlType = imageUrl + "_type";
                let imageUrlName = imageUrl + "_name";
                let driverForm = {};
                driverForm[imageUrl] = filePath;
                driverForm[imageUrlType] = imageTypeValue;
                driverForm[imageUrlName] = file.name;
                that.uploadPapersForm = Object.assign({}, that.uploadPapersForm, driverForm);

            },
            updateSuccess(response, file) {
                let that = this;
                let data = JSON.parse(response.data);
                let imageType = data['resultData']['imageType'];
                let imageTypeValue = data['resultData']['imageTypeValue'];
                let filePath = data['resultData']['filePath'];
                let imageUrl = imageType + "_imageUrl";
                let imageUrlType = imageUrl + "_type";
                let imageUrlName = imageUrl + "_name";
                let uploadForm = {};
                uploadForm[imageUrl] = filePath;
                uploadForm[imageUrlType] = imageTypeValue;
                uploadForm[imageUrlName] = file.name;
                that.uploadPapersForm = Object.assign({}, that.uploadPapersForm, uploadForm);

            },
            //获取添加的图片信息
            getAddCarRescueImgs: function (formObj, imgObjList) {
                let companyImgList = [];
                let that = this;
                let imgTypes = ["car_front_45", "driving_license_front", "driving_license_second",
                    "driving_license_back", "car_reg_cert", "traffic_insurance", "commercial_insurance"];
                imgTypes.forEach(function (key, index) {
                    if (formObj[key + '_imageUrl']) { //图片url
                        companyImgList.push(
                            {
                                pkId: that.findImagePkId(imgObjList, formObj[key + '_imageUrl']),
                                imageName: formObj[key + '_imageUrl_name'],
                                imagePath: formObj[key + '_imageUrl'],
                                type: formObj[key + '_imageUrl_type'],
                                imageMark: key
                            }
                        )
                    }
                });
                return companyImgList;
            },
            //查找图片的主键id
            findImagePkId(driverData, imageUrl) {
                let pkId = '';
                let that = this;
                if (driverData) {
                    let data = driverData.find(t =>
                        imageUrl.indexOf(t.imagePath) != -1
                    );
                    if (data) {
                        pkId = data.pkId;
                    }

                }

                return pkId;
            },
            /**
             *
             * @param form 赋值form
             * @param imgDataList 图片集合
             * @param imgPrefix 图片前缀
             */
            pottingRescueImgs(form, imgDataList, imgPrefix) { //把后台返回图片组装
                if (imgDataList && imgDataList.length > 0) {
                    imgDataList.forEach(item => {
                        let filePath = imgPrefix + "/" + item.imagePath;
                        let srcPath = item.imageMark + "_imageUrl";
                        let imageType = srcPath + "_type";
                        let imgName = srcPath + "_name";
                        form[srcPath] = filePath;
                        form[imageType] = item.type;
                        form[imgName] = item.imageName;
                    });
                }
            }

        },
        mounted() {
            var _this = this;
            window.onresize = function () { // 定义窗口大小变更通知事件
                _this.screenHeight = document.documentElement.clientHeight // 窗口高度
            }
        },
        watch: {
            uploadCarRescuePkId: function () {
                let that = this;
                let company = this.common.fetchData("company");
                this.companyId = company['pkId'];
                 that.$post("ltdCarRescue/queryCarRescue", {pkId: that.uploadCarRescuePkId, companyId: that.companyId}).then((response) => {
                    let respData = response.response;
                     if (response.code != 1) {
                         that.$message.error(response.msg);
                     } else if(response.code==1){
                         let dbRescue = respData.ltdCarRescue;
                         that.uploadPapersForm.pkId = dbRescue['pkId'];
                         that.uploadPapersForm.dlCarVin = dbRescue['dlCarVin'];
                         that.uploadPapersForm.ctaliNo = dbRescue['ctaliNo'];
                         that.uploadPapersForm.ciNo = dbRescue['ciNo'];
                         that.imgObjectList = respData.companyImgList;
                         that.pottingRescueImgs(that.uploadPapersForm, that.imgObjectList, respData.imgPrefix);
                    }

                }).catch(() => {
                     that.$message.error('获取车辆信息失败');
                });

            }
        }

    }
</script>

<style scoped>

</style>