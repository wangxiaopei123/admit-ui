<template>
    <div>
        <!--上传证件弹窗-->
        <el-dialog class="capacity-pop upload_pop capacity-pop-big capacity-line" title="上传车辆证件" :visible.sync="visible" :type="type" :pkid="pkId" width="650px" center :before-close="closeModal">
            <div class="capacity-pop-in" v-if="page===1">
                <el-form :model="uploadPapersForm" :rules="uploadPapersRules" ref="uploadPapersForm"
                         class="demo-ruleForm papers-item">

                    <el-form-item  class="upload_box" prop="driving_license_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>行驶证首页 </span>
                     <el-upload
                             class="avatar-uploader"
                             name="driving_license"
                             :action="action"
                             :show-file-list="false"
                             :http-request="requestUpload"
                             :on-success="handleAvatarSuccess"
                             :before-upload="common.beforeAvatarUpload">
                     
                         <img v-if="driving_license_imageUrl" :src="driving_license_imageUrl"
                              :imageType="driving_license_imageUrl_type"
                              :imgName="driving_license_imageUrl_name"
                              class="avatar">
                     
                         <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                     </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '12'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="driving_license_bywork_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>行驶证副页</span>
                        <el-upload
                               class="avatar-uploader"
                               name="driving_license_bywork"
                               :action="action"
                               :show-file-list="false"
                               :http-request="requestUpload"
                               :on-success="handleAvatarSuccess"
                               :before-upload="common.beforeAvatarUpload">
                       
                           <img v-if="driving_license_bywork_imageUrl" :src="driving_license_bywork_imageUrl"
                                :imageType="driving_license_bywork_imageUrl_type"
                                :imgName="driving_license_bywork_imageUrl_name"
                                class="avatar">
                       
                           <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                       </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '13'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="driving_license_back_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>行驶证背面</span>
                       <el-upload
                               class="avatar-uploader"
                               name="driving_license_back"
                               :action="action"
                               :show-file-list="false"
                               :http-request="requestUpload"
                               :on-success="handleAvatarSuccess"
                               :before-upload="common.beforeAvatarUpload">
                       
                           <img v-if="driving_license_back_imageUrl" :src="driving_license_back_imageUrl"
                                :imageType="driving_license_back_imageUrl_type"
                                :imgName="driving_license_back_imageUrl_name"
                                class="avatar">
                       
                           <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                       </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '14'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="transport_license_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>道路运输证</span>
                         <el-upload
                                        class="avatar-uploader"
                                        name="transport_license"
                                        :action="action"
                                        :show-file-list="false"
                                        :http-request="requestUpload"
                                        :on-success="handleAvatarSuccess"
                                        :before-upload="common.beforeAvatarUpload">
                                    <img v-if="transport_license_imageUrl" :src="transport_license_imageUrl"
                                         :imageType="transport_license_imageUrl_type"
                                         :imgName="transport_license_imageUrl_name"
                                         class="avatar">
                                    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                                </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '4'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="car_registration_imageUrl">
                        <span class="tit_tit">机动车登记证书</span>
                        <el-upload
                                class="avatar-uploader"
                                name="car_registration"
                                :action="action"
                                :show-file-list="false"
                                :http-request="requestUpload"
                                :on-success="handleAvatarSuccess"
                                :before-upload="common.beforeAvatarUpload">
                            <img v-if="car_registration_imageUrl" :src="car_registration_imageUrl"
                                 :imageType="car_registration_imageUrl_type"
                                 :imgName="car_registration_imageUrl_name"
                                 class="avatar">
                            <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                        </el-upload>
                        <div class="check_eg" @click="sampleImg = true,sampleType = '15'">查看示例</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="compulsory_insurance_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>交强险保单</span>
                       <el-upload
                              class="avatar-uploader"
                              name="compulsory_insurance"
                              :action="action"
                              :show-file-list="false"
                              :http-request="requestUpload"
                              :on-success="handleAvatarSuccess"
                              :before-upload="common.beforeAvatarUpload">
                      
                          <img v-if="compulsory_insurance_imageUrl" :src="compulsory_insurance_imageUrl"
                               :imageType="compulsory_insurance_imageUrl_type"
                               :imgName="compulsory_insurance_imageUrl_name"
                               class="avatar">
                      
                          <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                      </el-upload>
                        <div class="check_eg">&nbsp;</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="commercial_insurance_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>商业车险保单</span>
                       <el-upload
                               class="avatar-uploader"
                               name="commercial_insurance"
                               :action="action"
                               :show-file-list="false"
                               :http-request="requestUpload"
                               :on-success="handleAvatarSuccess"
                               :before-upload="common.beforeAvatarUpload">
                           <img v-if="commercial_insurance_imageUrl" :src="commercial_insurance_imageUrl"
                                :imageType="commercial_insurance_imageUrl_type"
                                :imgName="commercial_insurance_imageUrl_name"
                                class="avatar">
                           <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                       </el-upload>
                        <div class="check_eg">&nbsp;</div>
                    </el-form-item>
                    <el-form-item class="upload_box" prop="car_45_card_front_imageUrl">
                        <span class="tit_tit"><i class="not-null">*</i>车辆正面45°照片</span>
                        <el-upload
                               class="avatar-uploader"
                               name="car_45_card_front"
                               :action="action"
                               :show-file-list="false"
                               :http-request="requestUpload"
                               :on-success="handleAvatarSuccess"
                               :before-upload="common.beforeAvatarUpload">
                           <img v-if="car_45_card_front_imageUrl" :src="car_45_card_front_imageUrl"
                                :imageType="car_45_card_front_imageUrl_type"
                                :imgName="car_45_card_front_imageUrl_name"
                                class="avatar">
                           <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                       </el-upload>
                        <div style="position: relative;left: -10px;" class="check_eg" @click="sampleImg = true,sampleType = '16'">查看示例</div>
                    </el-form-item>
                    <div class="papers-sm">
                        <h2>上述证件要求</h2>
                        <ul>
                            <li>1、上述证件中所有信息清晰可见，字迹无PS、遮挡、涂改、模糊等情况</li>
                            <li>2、证件必须完整，证件四个边角需漏出，证件无残缺、断裂、破损等情况</li>
                            <li>3、必须为清晰、完整的彩色原件扫描件或数码照</li>
                            <li>4、支持上传图片格式-jpg/png/bmp,图片大小在3M以内</li>
                        </ul>
                    </div>
                    <div class="import-bottom">
                        <el-button @click="closeModal">取 消</el-button>
                        <el-button type="primary" @click="submitCarImage">下一步</el-button>
                    </div>

                </el-form>
            </div>
            <div class="capacity-pop-in pop-other"  v-else-if="page===2"><!--车头-->
                <p class="checkInfo-tip" style="margin-bottom: 0;">已为您自动识别部分信息，请仔细核对并完善</p>
                <el-form :model="checkCarHeadForm" :rules="checkCarHeadRules" ref="checkCarHeadForm" label-width="122px"
                         class="demo-ruleForm">
                    <el-input type="hidden" v-model="checkCarHeadForm.pkId"></el-input>
                    <div class="info-item clear">
                        <el-form-item label="车牌号码" prop="dlPlateNo">
                            <el-input v-model="checkCarHeadForm.dlPlateNo"></el-input>
                        </el-form-item>
                        <el-form-item label="所有人" prop="dlOwner">
                            <el-input v-model="checkCarHeadForm.dlOwner"></el-input>
                        </el-form-item>
                        <el-form-item label="使用性质" prop="dlUseNature">
                          <el-select v-model="checkCarHeadForm.dlUseNature"  placeholder="请选择">
                              <el-option :value=1 label="货运">货运</el-option>
                              <el-option :value=2 label="营运">营运</el-option>
                              <el-option :value=3 label="非营运">非营运</el-option>
                          </el-select>
                        </el-form-item>
                        <el-form-item label="车辆类型" prop="dlPlateType">
                            <el-select v-model="checkCarHeadForm.dlPlateType" placeholder="请选择">
                                <el-option :value=1 label="黄牌">黄牌</el-option>
                                <el-option :value=2 label="蓝牌">蓝牌</el-option>
                            </el-select>
                        </el-form-item>

                        <el-form-item label="车架号" prop="dlCarVin">
                            <el-input v-model="checkCarHeadForm.dlCarVin"></el-input>
                        </el-form-item>
                        <el-form-item label="品牌型号" prop="dlBrand">
                            <el-input v-model="checkCarHeadForm.dlBrand"></el-input>
                        </el-form-item>
                        <el-form-item label="注册日期" prop="dlRegisterTime">
                            <el-date-picker  v-model="checkCarHeadForm.dlRegisterTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="发动机号码" prop="dlEngineNo">
                            <el-input v-model="checkCarHeadForm.dlEngineNo"></el-input>
                        </el-form-item>
                        <el-form-item label="发证日期" prop="dlIssueTime">
                            <el-date-picker  v-model="checkCarHeadForm.dlIssueTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="整备质量" prop="dlHostlingWeight">
                            <el-input v-model="checkCarHeadForm.dlHostlingWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="核定载质量" prop="dlLoadWeight">
                            <el-input v-model="checkCarHeadForm.dlLoadWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="整准牵引质量" prop="dlTractionWeight">
                            <el-input v-model="checkCarHeadForm.dlTractionWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="外廓尺寸" prop="dlGabarite">
                            <el-input v-model="checkCarHeadForm.dlGabarite"></el-input>
                        </el-form-item>
                        <el-form-item label="强制报废日期止" prop="dlScrapEndTime">
                            <el-date-picker v-model="checkCarHeadForm.dlScrapEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="检验有效期止" prop="dlCheckEndTime">
                            <el-date-picker v-model="checkCarHeadForm.dlCheckEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                    </div>
                </el-form>
                <div class="import-bottom">
                    <el-button @click="page=1">上一步</el-button>
                    <el-button type="primary" @click="submitCarHeadForm">确 定</el-button>
                </div>
            </div>
            <div class="capacity-pop-in"  v-else-if="page===3">
                <p class="checkInfo-tip" style="margin-bottom: 0;">已为您自动识别部分信息，请仔细核对并完善</p>
                <el-form :model="checkCarTrailerForm" :rules="checkCarTrailerRules" ref="checkCarTrailerForm" label-width="122px"
                         class="demo-ruleForm">
                    <el-input type="hidden" v-model="checkCarTrailerForm.pkId"></el-input>
                    <div class="info-item clear">
                        <el-form-item label="挂车牌号" prop="dlPlateNo">
                            <el-input style="width: 85%;" type="text" v-model="checkCarTrailerForm.dlPlateNo"></el-input>&nbsp;&nbsp;挂
                        </el-form-item>
                        <el-form-item label="所有人" prop="dlBelongUser">
                            <el-input v-model="checkCarTrailerForm.dlBelongUser"></el-input>
                        </el-form-item>
                        <el-form-item label="车辆类型" prop="dlCarType">
                            <el-input v-model="checkCarTrailerForm.dlCarType"></el-input>
                        </el-form-item>
                        <el-form-item label="使用性质" prop="dlUseNature">
                            <el-select v-model="checkCarTrailerForm.dlUseNature" placeholder="请选择">
                                <el-option :value=1 label="货运">货运</el-option>
                                <el-option :value=2 label="营运">营运</el-option>
                                <el-option :value=3 label="非营运">非营运</el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="品牌型号" prop="dlBrand">
                            <el-input v-model="checkCarTrailerForm.dlBrand"></el-input>
                        </el-form-item>
                        <el-form-item label="车架号" prop="dlCarVin">
                            <el-input v-model="checkCarTrailerForm.dlCarVin"></el-input>
                        </el-form-item>

                        <el-form-item label="注册日期" prop="dlRegisterTime">
                            <el-date-picker v-model="checkCarTrailerForm.dlRegisterTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="发证日期" prop="dlIssueTime">
                            <el-date-picker  v-model="checkCarTrailerForm.dlIssueTime"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="整备质量" prop="dlHostlingWeight">
                            <el-input v-model="checkCarTrailerForm.dlHostlingWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="核定载质量" prop="dlLoadWeight">
                            <el-input v-model="checkCarTrailerForm.dlLoadWeight"></el-input>
                        </el-form-item>
                        <el-form-item label="外廓尺寸" prop="dlGabarite">
                            <el-input v-model="checkCarTrailerForm.dlGabarite"></el-input>
                        </el-form-item>
                        <el-form-item label="检验有效期止" prop="dlCheckEndTime">
                            <el-date-picker v-model="checkCarTrailerForm.dlCheckEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item label="强制报废日期止" prop="dlScrapEndTime">
                            <el-date-picker v-model="checkCarTrailerForm.dlScrapEndTime"
                                            type="date"
                                            placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                    </div>
                </el-form>
                <div class="import-bottom">
                    <el-button @click="page=1">上一步</el-button>
                    <el-button type="primary" @click="submitCarTrailerForm">确 定</el-button>
                </div>
            </div><!--挂车-->
        </el-dialog>
        <SampleGraph :visible.sync="sampleImg" :sampleType="sampleType"></SampleGraph>
    </div>
</template>

<script>
    import SampleGraph from '../../SampleGraph'  //示例图
    export default {
        inject:['reload'],
        components: {
            'SampleGraph':SampleGraph,
        },
        data(){

            return{
                imageUrl:"",
                sampleImg: false,
                sampleType:'',
                uploadPapersForm:{
					car_45_card_front_imageUrl: '',  // 图片
					driving_license_imageUrl: '',
					driving_license_bywork_imageUrl: '',
					driving_license_back_imageUrl: '',
					transport_license_imageUrl: '',
					compulsory_insurance_imageUrl: '',
					commercial_insurance_imageUrl: '',
				},
                uploadPapersRules:{
					car_45_card_front_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
					driving_license_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
					driving_license_bywork_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
					driving_license_back_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
					transport_license_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
					compulsory_insurance_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
					commercial_insurance_imageUrl: [{required: true, message: '请上传图片', trigger: 'change'}],
				},
                checkCarHeadForm:{
                    pkId:this.pkId
                },
                checkCarHeadRules:{
                    dlPlateNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlOwner: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlUseNature: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlPlateType: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlCarVin: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlBrand: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlRegisterTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlPlateNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlEngineNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlIssueTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlHostlingWeight: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlLoadWeight: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlTractionWeight: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlGabarite: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlScrapEndTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlCheckEndTime: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                },
                checkCarTrailerForm:{
                    pkId:this.pkId
                },
                checkCarTrailerRules:{
                    dlPlateNo: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlBelongUser: [{required: true, message: '此项不能为空', trigger: 'blur'}],
                    dlCarType: [{required: true, message: '此项不能为空', trigger: 'blur'}],
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
                page:1, //步骤
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
                imgdata:"",
            }
        },
        props: {
            visible: {
                type: Boolean,
                default: true
            },
            type: {
                type: Number,
                default: 1
            },
            pkId: {
                type: String,
                default: ""
            }

        },
        methods:{
            closeModal: function () {
                this.reload();
            },
            submitCarImage(){
                console.error("1111")
                this.$refs.uploadPapersForm.validate((valid) => {
                    console.error(valid)
                    if (valid == false) {
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
                        that.imgdata = JSON.stringify(companyImgList);
                        console.error(that.imgdata)
                        if(that.type == 1){
                            console.error(that.imgdata)
                            that.page = 2;
                        }
                        if(that.type == 2){
                            console.error(that.imgdata)
                            that.page=3;
                        }
                    }
                })
            },
            submitCarHeadForm(){
                let that=this;
                let data = new FormData();
                data = JSON.stringify(this.checkCarHeadForm);
                that.$post("ltdCarHeadstock/saveCarBasic", {
                    "data": "{ltdCarHeadstock:" + data + "}",
                    "imgData": that.imgdata
                }).then(function (response) {
                    if(response.code==0){
                        alert(response.msg)
                    }else  if(response.code==1){
                        that.$message({
                            type: 'success',
                            message: '保存成功!'
                        });
                        that.reload();
                    }
                })
            },
            submitCarTrailerForm(){
                let that=this;
                let data = new FormData();
                data = JSON.stringify(this.addHeadstockForm);
                that.$post("ltdCarTrailer/saveTrailerBasic", {"data": "{ltdCarTrailer:" + data + "}","imgData": that.imgdata}).then(function (response) {
                    if(response.code==0){
                        alert(response.msg)
                    }else  if(response.code==1){
                        that.$message({
                            type: 'success',
                            message: '保存成功!'
                        });
                        that.reload();
                    }
                })
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
            },
            requestUpload(obj) {
                obj.companyId = this.common.fetchData("company").pkId;
                this.common.uploadImgFun(obj, this);
            },

            /*************图片处理----end************/
        },watch:{
            pkId:function () {
                this.checkCarHeadForm.pkId=this.pkId;
                this.checkCarTrailerForm.pkId=this.pkId;
            }
        }
    }
</script>

<style scoped>

</style>