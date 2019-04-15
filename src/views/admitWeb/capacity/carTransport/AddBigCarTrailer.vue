<template>
    <div> <!--添加车头弹窗-->
        <el-dialog class="capacity-pop capacity-pop-big capacity-line" title="添加挂车" :visible.sync="visible" :pkId="pkId" center
                   :before-close="closeModal">
            <div class="capacity-pop-in">
                <div class="steps steps-step">
                    <el-steps :active="activePop" finish-status="success" process-status="finish" align-center>
                        <el-step title="添加车辆信息"></el-step>
                        <el-step title="核对并完善信息"></el-step>
                        <el-step title="添加成功"></el-step>
                    </el-steps>
                </div>
                <el-form v-if="activePop === 0" :model="addHeadstockForm" :rules="addHeadstockRules"
                         ref="addHeadstockForm" label-width="140px"
                         class="demo-ruleForm">
                    <h2 class="info-title" style="margin-bottom: 10px;">基本信息</h2>

                    <el-input v-model="addHeadstockForm.pkId" type="hidden" prop="pkId"></el-input>


                    <div class="info-item clear">
                        <el-form-item label="板位数" prop="plateNum">
                            <el-tooltip placement="bottom">
                                <div slot="content">
                                    此处填写的为车头板位数，请勿将车头与挂车的板位数填写到一起
                                </div>
                                <el-select v-model="addHeadstockForm.plateNum" placeholder="请选择">
                                    <el-option :value=4 label="4"></el-option>
                                    <el-option :value=5 label="5"></el-option>
                                    <el-option :value=6 label="6"></el-option>
                                    <el-option :value=7 label="7"></el-option>
                                    <el-option :value=8 label="8"></el-option>
                                </el-select>
                            </el-tooltip>
                        </el-form-item>
                        <el-form-item label="车辆正面45°照" class="required_flag">
                            <div class="upload_box">
                                <el-upload
                                        class="avatar-uploader"
                                        name="car_45_card_front"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="car_45_card_front_imageUrl" :src="car_45_card_front_imageUrl"
                                         :imageType="car_45_card_front_imageUrl_type"
                                         :imgName="car_45_card_front_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg" @click="sampleImg = true,sampleType = '21'">查看示例</div>
                            </div>
                        </el-form-item>
                    </div>
                    <h2 class="info-title">行驶证信息</h2>
                    <div class="info-item clear">
                        <el-form-item label="挂车牌号" prop="dlPlateNo">
                            <el-input style="width: 91%;" type="text" v-model="addHeadstockForm.dlPlateNo"></el-input>&nbsp;&nbsp;挂
                        </el-form-item>
                        <el-form-item label="所有人" prop="dlBelongUser">
                            <el-tooltip placement="bottom">
                                <div slot="content">
                                    所有人必须与企业名称一致
                                </div>
                                <el-input v-model="addHeadstockForm.dlBelongUser"></el-input>
                            </el-tooltip>
                           <!-- <span class="plateNo">车牌号码<i>去关联</i></span>-->
                        </el-form-item>
                        <el-form-item label="证件照片" class="required_flag">
                            <div class="upload_box">
                                <span class="tit_tit">行驶证首页</span>
                                <el-upload
                                        class="avatar-uploader"
                                        name="driving_license"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="driving_license_imageUrl" :src="driving_license_imageUrl"
                                         :imageType="driving_license_imageUrl_type"
                                         :imgName="driving_license_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg" @click="sampleImg = true,sampleType = '17'">查看示例</div>
                            </div>
                            <div class="upload_box">
                                <span class="tit_tit">行驶副业</span>
                                <el-upload
                                        class="avatar-uploader"
                                        name="driving_license_bywork"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="driving_license_bywork_imageUrl" :src="driving_license_bywork_imageUrl"
                                         :imageType="driving_license_bywork_imageUrl_type"
                                         :imgName="driving_license_bywork_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg" @click="sampleImg = true,sampleType = '18'">查看示例</div>
                            </div>
                            <div class="upload_box">
                                <span class="tit_tit">行驶证背面</span>
                                <el-upload
                                        class="avatar-uploader"
                                        name="driving_license_back"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="driving_license_back_imageUrl" :src="driving_license_back_imageUrl"
                                         :imageType="driving_license_back_imageUrl_type"
                                         :imgName="driving_license_back_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg" @click="sampleImg = true,sampleType = '19'">查看示例</div>
                            </div>
                        </el-form-item>
                        <el-form-item label="机动车登记证书">
                            <div class="upload_box">
                                <el-upload
                                        class="avatar-uploader"
                                        name="car_registration"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="car_registration_imageUrl" :src="car_registration_imageUrl"
                                         :imageType="car_registration_imageUrl_type"
                                         :imgName="car_registration_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg" @click="sampleImg = true,sampleType = '20'">查看示例</div>
                            </div>
                        </el-form-item>
                    </div>
                    <h2 class="info-title">运输许可证信息</h2>
                    <div class="info-item clear">
                        <el-form-item label="业户名称" prop="rpOwnerName">
                            <el-input v-model="addHeadstockForm.rpOwnerName"></el-input>
                        </el-form-item>
                        <el-form-item label="所属省份" prop="rpProId">
                            <el-select v-model="addHeadstockForm.rpProId" placeholder="请选择省">
                                <el-option
                                        v-for="item in provinceOption"
                                        :key="item.regionId"
                                        :label="item.name"
                                        :value="item.regionId">
                                </el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="运输许可证号" prop="rpNo">
                            <el-input v-model="addHeadstockForm.rpNo"></el-input>
                        </el-form-item>
                        <el-form-item label="发证日期" prop="rpTime">
                            <el-date-picker v-model="addHeadstockForm.rpTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="运输许可证" class="required_flag">
                            <div class="upload_box">
                                <el-upload
                                        class="avatar-uploader"
                                        name="transport_license"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="transport_license_imageUrl" :src="transport_license_imageUrl"
                                         :imageType="transport_license_imageUrl_type"
                                         :imgName="transport_license_imageUrl_name"
                                         class="avatar">
                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg" @click="sampleImg = true,sampleType = '4'">查看示例</div>
                            </div>
                        </el-form-item>
                        <el-form-item class="termOfValidity required_flag" label="有效期">
                            <el-form-item prop="rpStartTime">
                            <el-date-picker v-model="addHeadstockForm.rpStartTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                            </el-form-item>
                            <span>至</span>
                            <el-form-item prop="rpEndTime">
                            <el-date-picker v-model="addHeadstockForm.rpEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                            </el-form-item>
                        </el-form-item>

                    </div>
                    <h2 class="info-title">车辆保险信息</h2>
                    <div class="info-item clear">
                        <el-form-item label="是否有交强险" prop="isCtali">
                            <el-radio-group v-model="addHeadstockForm.isCtali">
                                <el-radio value="1" :label="1">有</el-radio>
                                <el-radio value="0" :label="0">无</el-radio>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item label="是否有商业险" prop="isCi">
                            <el-radio-group v-model="addHeadstockForm.isCi">
                                <el-radio value="1" :label="1">有</el-radio>
                                <el-radio value="0" :label="0">无</el-radio>
                            </el-radio-group>
                        </el-form-item>
                    </div>
                    <div class="info-item clear" v-if="addHeadstockForm.isCtali === 1">
                        <el-form-item label="交强险保险品牌" prop="ctaliType">
                            <el-select v-model="addHeadstockForm.ctaliType" placeholder="请选择">
                                <el-option v-for="item in ctaliTypeOption"
                                           :key="item.value"
                                           :label="item.name"
                                           :value="item.value">
                                </el-option>

                            </el-select>
                        </el-form-item>
                        <el-form-item label="交强险保险单号" prop="ctaliNo">
                            <el-input v-model="addHeadstockForm.ctaliNo"></el-input>
                        </el-form-item>
                        <el-form-item label="保险单照片" class="required_flag">
                            <div class="upload_box">
                                <el-upload
                                        class="avatar-uploader"
                                        name="compulsory_insurance"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="compulsory_insurance_imageUrl" :src="compulsory_insurance_imageUrl"
                                         :imageType="compulsory_insurance_imageUrl_type"
                                         :imgName="compulsory_insurance_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg">&nbsp;</div>
                            </div>
                        </el-form-item>
                        <el-form-item class="termOfValidity required_flag" label="交强险有效期">
                            <el-form-item prop="ctaliStartTime">
                            <el-date-picker
                                    type="date" v-model="addHeadstockForm.ctaliStartTime"
                                    placeholder="选择日期">
                            </el-date-picker>
                            </el-form-item>
                            <span>至</span>
                            <el-form-item prop="ctaliEndTime">
                            <el-date-picker
                                    type="date" v-model="addHeadstockForm.ctaliEndTime"
                                    placeholder="选择日期">
                            </el-date-picker>
                            </el-form-item>
                        </el-form-item>
                    </div>
                    <div class="info-item clear" v-if="addHeadstockForm.isCi  === 1">
                        <el-form-item label="商业险保险品牌" prop="ciType">
                            <el-select v-model="addHeadstockForm.ciType" placeholder="请选择">
                                <el-option v-for="item in ciTypeOption"
                                           :key="item.value"
                                           :label="item.name"
                                           :value="item.value">
                                </el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="商业险保险单号" prop="ciNo">
                            <el-input v-model="addHeadstockForm.ciNo"></el-input>
                        </el-form-item>
                        <el-form-item label="保险单照片" class="required_flag">
                            <div class="upload_box">
                                <el-upload
                                        class="avatar-uploader"
                                        name="commercial_insurance"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="beforeAvatarUpload">

                                    <img v-if="commercial_insurance_imageUrl" :src="commercial_insurance_imageUrl"
                                         :imageType="commercial_insurance_imageUrl_type"
                                         :imgName="commercial_insurance_imageUrl_name"
                                         class="avatar">

                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                                <div class="check_eg">&nbsp;</div>
                            </div>
                        </el-form-item>
                        <el-form-item class="termOfValidity required_flag" label="商业险有效期">
                            <el-form-item prop="ciStartTime">
                            <el-date-picker v-model="addHeadstockForm.ciStartTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                            </el-form-item>
                            <span>至</span>
                            <el-form-item prop="ciEndTime">
                            <el-date-picker v-model="addHeadstockForm.ciEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                            </el-form-item>
                        </el-form-item>
                    </div>
                    <div class="import-bottom">
                        <el-button @click="closeModal">取 消</el-button>
                        <el-button type="primary" @click="submitAddHeadstockForm">下一步</el-button>
                    </div>
                </el-form>


                <el-form v-if="activePop === 1" :model="addHeadstockForm" :rules="addHeadstockRules"
                         ref="addHeadstockForm" label-width="140px" class="demo-ruleForm">
                    <p class="checkInfo-tip" style="margin-bottom: 0;">已为您自动识别部分信息，请仔细核对并完善</p>
                    <el-input v-model="addHeadstockForm.pkId" type="hidden"></el-input>
                    <div class="info-item clear">
                        <el-form-item label="挂车牌号" prop="dlPlateNo">
                            <el-input style="width: 91%;" v-model="addHeadstockForm.dlPlateNo"></el-input>&nbsp;&nbsp;挂
                        </el-form-item>
                        <el-form-item label="所有人" prop="dlBelongUser">
                            <el-tooltip placement="bottom">
                                <div slot="content">
                                    所有人必须与企业名称一致
                                </div>
                                <el-input v-model="addHeadstockForm.dlBelongUser"></el-input>
                            </el-tooltip>
                        </el-form-item>
                        <el-form-item label="车辆类型" prop="dlCarType">
                            <el-input v-model="addHeadstockForm.dlCarType"></el-input>
                        </el-form-item>
                        <el-form-item label="使用性质" prop="dlUseNature">
                            <el-select v-model="addHeadstockForm.dlUseNature" placeholder="请选择">
                                <el-option :value=1 label="货运">货运</el-option>
                                <el-option :value=2 label="营运">营运</el-option>
                                <el-option :value=3 label="非营运">非营运</el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="品牌型号" prop="dlBrand">
                            <el-input v-model="addHeadstockForm.dlBrand"></el-input>
                        </el-form-item>
                        <el-form-item label="车架号" prop="dlCarVin">
                            <el-input v-model="addHeadstockForm.dlCarVin"></el-input>
                        </el-form-item>
                        <el-form-item label="注册日期" prop="dlRegisterTime">
                            <el-date-picker v-model="addHeadstockForm.dlRegisterTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="发证日期" prop="dlIssueTime">
                            <el-date-picker v-model="addHeadstockForm.dlIssueTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="整备质量" prop="dlHostlingWeight">
                            <el-input v-model="addHeadstockForm.dlHostlingWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="核定载质量" prop="dlLoadWeight">
                            <el-input v-model="addHeadstockForm.dlLoadWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="外廓尺寸" prop="dlGabarite">
                            <el-input v-model="addHeadstockForm.dlGabarite"></el-input>
                        </el-form-item>
                        <el-form-item label="检验有效期止" prop="dlCheckEndTime">
                            <el-date-picker v-model="addHeadstockForm.dlCheckEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="强制报废日期止" prop="dlScrapEndTime">
                            <el-date-picker v-model="addHeadstockForm.dlScrapEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                    </div>
                    <div class="import-bottom">
                        <el-button @click="activePop = 0">上一步</el-button>
                        <el-button type="primary" @click="submitAddHeadstockForm2">确 定</el-button>
                    </div>
                </el-form>

            </div>
        </el-dialog>
        <SampleGraph :visible.sync="sampleImg" :sampleType="sampleType"></SampleGraph>
    </div>
</template>

<script>
    import SampleGraph from '../../SampleGraph'  //示例图
    export default {
        inject:['reload'],
        components:{
            'SampleGraph':SampleGraph
        },

        data() {

            return {
                sampleImg: false,
                sampleType:'',
                activePop: 0,   //表单显示
                provinceOption: [],
                ctaliTypeOption: [],
                ciTypeOption: [],
                addHeadstockForm: {
                    car_45_card_front_imageUrl: '',  // 图片
                    driving_license_imageUrl: '',
                    driving_license_bywork_imageUrl: '',
                    driving_license_back_imageUrl: '',
                    transport_license_imageUrl: '',
                    compulsory_insurance_imageUrl: '',
                    commercial_insurance_imageUrl: '',
                    rpProName :'',
                    dlCarType : '',
                    dlBelongUser : '',

                    dlPlateNo : '',
                    dlOwner : '',
                    dlUseNature : '',
                    dlBrand : '',
                    dlEngineNo : '',
                    dlCarVin : '',
                    dlRegisterTime : '',
                    dlIssueTime : '',
                    dlHostlingWeight : '',
                    dlCheckEndTime : '',
                    dlLoadWeight : '',
                    dlScrapEndTime : '',
                    dlGabarite : '',
                    dlTractionWeight : '',
                },
                addHeadstockRules: {

                    car_45_card_front_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
                    driving_license_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
                    driving_license_bywork_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
                    driving_license_back_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
                    transport_license_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
                    compulsory_insurance_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
                    commercial_insurance_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],

                    plateNum: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlPlateNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlBelongUser: [{required: true, message: '此项不能为空', trigger: 'blur'}],

                    rpOwnerName: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    rpProId: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    rpNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    rpTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    rpStartTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    rpEndTime:[{required: true, message: '此项不能为空', trigger: 'blur'}],
                    isCtali: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    isCi: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ctaliType: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ctaliNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ctaliStartTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ctaliEndTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ciType: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ciNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ciStartTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    ciEndTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    /******下一步********/
                    dlPlateNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlBelongUser: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlPlateType: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlCarType: [{required: true, message: '车辆类型不能为空', trigger: 'blur'}],
                    dlUseNature: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlBrand: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlCarVin: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlRegisterTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlIssueTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlHostlingWeight: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlLoadWeight: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlGabarite: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlCheckEndTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlScrapEndTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                },
                imageUrl: "",//暂时
                action: this.common.CONSTANT.UPLOADIMGPATH + 'recognizeImage',//上传图片地址
                //车辆正面45°照=图片地址
                car_45_card_front_imageUrl: '',
                car_45_card_front_imageUrl_type: '',
                car_45_card_front_imageUrl_name: "",
                //行驶证首页
                driving_license_imageUrl: '',
                driving_license_imageUrl_type: '',
                driving_license_imageUrl_name: "",
                //行驶副业
                driving_license_bywork_imageUrl: "",
                driving_license_bywork_imageUrl_type: "",
                driving_license_bywork_imageUrl_name: "",
                // 行驶证背面
                driving_license_back_imageUrl: "",
                driving_license_back_imageUrl_type: "",
                driving_license_back_imageUrl_name: "",
                //机动车登记证书
                car_registration_imageUrl: "",
                car_registration_imageUrl_type: "",
                car_registration_imageUrl_name: "",
                //运输许可
                transport_license_imageUrl: "",
                transport_license_imageUrl_type: "",
                transport_license_imageUrl_name: "",
                //交强险
                compulsory_insurance_imageUrl: "",
                compulsory_insurance_imageUrl_type: "",
                compulsory_insurance_imageUrl_name: "",
                //商业保险
                commercial_insurance_imageUrl: "",
                commercial_insurance_imageUrl_type: "",
                commercial_insurance_imageUrl_name: "",
            }
        },
        props: {
            visible: {
                type: Boolean,
                default: false
            },
            pkId: {
                type: String,
                default: false
            }

        },
        created: function () {
            //  let that = this;
            this.initProvince();
            this.common.getBizConstants(this, 'ctaliType', 'ctaliTypeOption');
            this.common.getBizConstants(this, 'ctaliType', 'ciTypeOption');

        },
        methods: {
            //初始化城市
            initProvince: function () {
                this.common.initProvince(this, ["provinceOption"])
            },
            closeModal: function () {
                this.reload();
            },
            /*************图片处理----start************/
            handleAvatarSuccess(res, file) {
                let data = JSON.parse(res.data);
                let imageType = data['resultData']['imageType'];
                let imageTypeValue = data['resultData']['imageTypeValue'];
                let filePath = data['resultData']['filePath'];
                let imageUrl = imageType + "_imageUrl";
                let imageUrlType = imageUrl + "_type";
                let imageUrlName = imageUrl + "_name";
                this[imageUrl] = filePath;
                this[imageUrlType] = imageTypeValue;
                this[imageUrlName] = file.name;

                let attrs = data['resultData']['attrs']; //ocr识别结果
                if (attrs) {
                    if ("driving_license" === imageType) { //行驶证正面
                        this.addHeadstockForm.dlPlateNo = attrs['vehiclePlateNumber'];          // 车牌号码
                        this.addHeadstockForm.dlCarType = attrs['vehicleType'];                 // 车辆类型
                        this.addHeadstockForm.dlOwner = attrs['vehicleOwner'];                  // 所有人
                        let useNature = attrs['vehicleUseCharacter'];
                        let dlUseNature = 0;
                        if (useNature == '货运') {
                            dlUseNature = 1;
                        } else if (useNature == '营运') {
                            dlUseNature = 2;
                        } else if (useNature == '非营运') {
                            dlUseNature = 3;
                        }
                        this.addHeadstockForm.dlUseNature = dlUseNature;       // 使用性质
                        this.addHeadstockForm.dlBrand = attrs['vehicleModel'];                  // 品牌型号
                        this.addHeadstockForm.dlEngineNo = attrs['vehicleEngineNumber'];        // 发动机号码
                        this.addHeadstockForm.dlCarVin = attrs['vehicleVinNumber'];             // 车架号
                        this.addHeadstockForm.dlRegisterTime = attrs['vehicleRegisterDate'];    // 注册日期
                        this.addHeadstockForm.dlIssueTime = attrs['vehicleIssueDate'];          // 发证日期
                    } else if ("driving_license_back" === imageType) {//行驶证背面
                        this.addHeadstockForm.dlHostlingWeight = attrs['vehicleCurbWeight'];                // 整备质量
                        this.addHeadstockForm.dlCheckEndTime = attrs['vehicleEffectiveUntil'];              // 检验有效期止
                        this.addHeadstockForm.dlLoadWeight = attrs['vehicleLoadrWeight'];                   // 核定载质量
                        this.addHeadstockForm.dlScrapEndTime = attrs['vehicleNote'];                        // 强制报废日期止
                        this.addHeadstockForm.dlGabarite = attrs['vehicleOutSize'];                         // 外廓尺寸
                        this.addHeadstockForm.dlTractionWeight = attrs['vehicleTowWeight'];                 // 准牵引质量
                    }
                }
            },
            requestUpload(obj) {
                obj.companyId = this.common.fetchData("company").pkId;
                this.common.uploadImgFun(obj, this);
            },
            beforeAvatarUpload(file) {
                const isJPG = file.type === 'image/jpg';
                const isJPEG = file.type === 'image/jpeg';
                const isPNG = file.type === 'image/png';
                const isBMP = file.type === 'image/bmp';
                const isLt2M = file.size / 1024 / 1024 < 5;
                if (!isJPG && !isJPEG && !isPNG && !isBMP) {
                    this.$message.error('上传图片只能是 JPG/PNG/BMP 格式!');
                    return false;
                }
                if (!isLt2M) {
                    this.$message.error('上传图片大小不能超过 2MB!');
                    return false;
                }
                return true;
            },
            /*************图片处理----end************/
            submitAddHeadstockForm() {
                this.$refs.addHeadstockForm.validate((valid) => {
                    if (valid) {
                        let data = new FormData();
                        let imgdata = new FormData();
                        let that = this;
                        let companyImgList = [];
                        if (this['car_45_card_front_imageUrl']) { //45度照片
                            companyImgList.push(
                                {
                                    imageName: this['car_45_card_front_imageUrl_name'],
                                    imagePath: this['car_45_card_front_imageUrl'],
                                    type: this['car_45_card_front_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'car_45_card_front'
                                }
                            )
                        }
                        if (this['driving_license_imageUrl']) { //行驶证首页
                            companyImgList.push(
                                {
                                    imageName: this['driving_license_imageUrl_name'],
                                    imagePath: this['driving_license_imageUrl'],
                                    type: this['driving_license_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'driving_license'
                                }
                            )
                        }
                        if (this['driving_license_bywork_imageUrl']) { //行驶副业
                            companyImgList.push(
                                {
                                    imageName: this['driving_license_bywork_imageUrl_name'],
                                    imagePath: this['driving_license_bywork_imageUrl'],
                                    type: this['driving_license_bywork_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'driving_license_bywork'
                                }
                            )
                        }
                        if (this['driving_license_back_imageUrl']) { //行驶证背面
                            companyImgList.push(
                                {
                                    imageName: this['driving_license_back_imageUrl_name'],
                                    imagePath: this['driving_license_back_imageUrl'],
                                    type: this['driving_license_back_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'driving_license_back'
                                }
                            )
                        }
                        if (this['car_registration_imageUrl']) { //机动车登记证书
                            companyImgList.push(
                                {
                                    imageName: this['car_registration_imageUrl_name'],
                                    imagePath: this['car_registration_imageUrl'],
                                    type: this['car_registration_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'car_registration'
                                }
                            )
                        }
                        if (this['transport_license_imageUrl']) { //运输许可
                            companyImgList.push(
                                {
                                    imageName: this['transport_license_imageUrl_name'],
                                    imagePath: this['transport_license_imageUrl'],
                                    type: this['transport_license_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'transport_license'
                                }
                            )
                        }
                        if (this['compulsory_insurance_imageUrl']) { //交强险
                            companyImgList.push(
                                {
                                    imageName: this['compulsory_insurance_imageUrl_name'],
                                    imagePath: this['compulsory_insurance_imageUrl'],
                                    type: this['compulsory_insurance_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'compulsory_insurance'
                                }
                            )
                        }
                        if (this['commercial_insurance_imageUrl']) { //商业保险
                            companyImgList.push(
                                {
                                    imageName: this['commercial_insurance_imageUrl_name'],
                                    imagePath: this['commercial_insurance_imageUrl'],
                                    type: this['commercial_insurance_imageUrl_type'],
                                    imageStatus: 0,
                                    imageMark: 'commercial_insurance'
                                }
                            )
                        }
                        that.addHeadstockForm.rpProName = that.common.getProvinceName(that, that.addHeadstockForm.rpProId, that.provinceOption),
                        data = JSON.stringify(this.addHeadstockForm);
                        imgdata = JSON.stringify(companyImgList);
                        that.$post("ltdCarTrailer/saveTrailerBasic", {"data": "{ltdCarTrailer:" + data + "}","imgData": imgdata}).then(function (response) {
                            if(response.code==0){
                                alert(response.msg)
                            }else  if(response.code==1){
                                that.addHeadstockForm.pkId=response.response;
                                that.activePop = 1;
                            }
                        })

                    }
                })
            },
            submitAddHeadstockForm2() {
                this.$refs.addHeadstockForm.validate((valid) => {
                    if (valid) {
                        let data = new FormData();
                        let that = this;
                        data = JSON.stringify(this.addHeadstockForm);
                        that.$post("ltdCarTrailer/saveTrailerVerify", {"data": "{ltdCarTrailer:" + data + "}"}).then(function (response) {
                            that.$message({
                                type: 'success',
                                message: '保存成功!'
                            });
                            that.reload();
                        })
                    }
                })
            }
        },
        watch: {
            pkId: function () {
                let that = this;
                that.$get("ltdCarTrailer/selectOne", {"pkId": that.pkId}).then(function (response) {
                    if (response.response != null) {
                        that.addHeadstockForm = response.response.ltdCarTrailer;
                        that.addHeadstockForm.rpProId=Number(that.addHeadstockForm.rpProId);//绑定省
                        if (response.response.ltdCompanyImgs.length > 0) {
                            response.response.ltdCompanyImgs.forEach(function (image) {
                                let imageMark = image['imageMark'];
                                let imageType = imageMark + "_imageUrl_type";
                                let imageName = imageMark + "_imageUrl_name";
                                let imageUrl = imageMark + "_imageUrl";
                                that[imageMark]=image.imageMark;
                                that[imageType]=image.type;
                                that[imageName]=image.imageName;
                                that[imageUrl]=that.common.CONSTANT.imagePrefix+image.imagePath;
                                that.addHeadstockForm[imageUrl]=image.imagePath;
                            })
                        }
                    }

                })
            }
        }
    }
</script>

<style scoped>

</style>
