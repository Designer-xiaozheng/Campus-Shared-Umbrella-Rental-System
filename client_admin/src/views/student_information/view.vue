<template>
	<el-main class="bg edit_wrap">
		<el-form ref="form" :model="form" status-icon label-width="120px" v-if="is_view()">

							<el-col v-if="user_group === '管理员' || $check_field('get','student_photos') || $check_field('add','student_photos') || $check_field('set','student_photos')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生照片" prop="student_photos">
								<el-upload :disabled="disabledObj['student_photos_isDisabled']" id="student_photos" class="avatar-uploader" drag
						accept="image/gif, image/jpeg, image/png, image/jpg" action="" :http-request="upload_student_photos"
						:show-file-list="false" v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','student_photos')) || (!form['student_information_id'] && $check_field('add','student_photos'))">
						<img v-if="form['student_photos']" :src="$fullUrl(form['student_photos'])" class="avatar">
						<i v-else class="el-icon-plus avatar-uploader-icon"></i>
					</el-upload>
					<el-image v-else-if="$check_field('get','student_photos')" style="width: 100px; height: 100px"
						:src="$fullUrl(form['student_photos'])" :preview-src-list="[$fullUrl(form['student_photos'])]">
						<div slot="error" class="image-slot">
							<img src="../../../public/img/error.png" style="width: 90px; height: 90px" />
						</div>
					</el-image>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_account') || $check_field('add','student_account') || $check_field('set','student_account')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生账号" prop="student_account">
																		<div v-if="user_group !== '管理员'">
							{{ get_user_session_student_account(form['student_account']) }}
							<!--<el-input id="business_name" v-model="form['student_account']" placeholder="请输入学生账号"-->
							<!--v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','student_account')) || (!form['student_information_id'] && $check_field('add','student_account'))" :disabled="disabledObj['student_account_isDisabled']"></el-input>-->
							<!--<div v-else-if="$check_field('get','student_account')">{{form['student_account']}}</div>-->
							<el-select v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','student_account')) || (!form['student_information_id'] && $check_field('add','student_account'))" id="student_account" v-model="form['student_account']" :disabled="disabledObj['student_account_isDisabled']">
								<el-option v-for="o in list_user_student_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
										   :value="o['user_id']">
								</el-option>
							</el-select>
							<el-select v-else-if="$check_field('get','student_account')" id="student_account" v-model="form['student_account']" :disabled="true">
								<el-option v-for="o in list_user_student_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
										   :value="o['user_id']">
								</el-option>
							</el-select>
						</div>
						<el-select v-else id="student_account" v-model="form['student_account']" :disabled="disabledObj['student_account_isDisabled']">
							<el-option v-for="o in list_user_student_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
									   :value="o['user_id']">
							</el-option>
						</el-select>
																</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_name') || $check_field('add','student_name') || $check_field('set','student_name')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生姓名" prop="student_name">
												<el-input id="student_name" v-model="form['student_name']" placeholder="请输入学生姓名"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','student_name')) || (!form['student_information_id'] && $check_field('add','student_name'))" :disabled="disabledObj['student_name_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','student_name')">{{form['student_name']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_no') || $check_field('add','student_no') || $check_field('set','student_no')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生学号" prop="student_no">
												<el-input id="student_no" v-model="form['student_no']" placeholder="请输入学生学号"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','student_no')) || (!form['student_information_id'] && $check_field('add','student_no'))" :disabled="disabledObj['student_no_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','student_no')">{{form['student_no']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','gender') || $check_field('add','gender') || $check_field('set','gender')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="性别" prop="gender">
								<el-select id="gender" v-model="form['gender']"
						v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','gender')) || (!form['student_information_id'] && $check_field('add','gender'))">
						<el-option v-for="o in list_gender" :key="o" :label="o" :value="o">
						</el-option>
					</el-select>
					<div v-else-if="$check_field('get','gender')">{{form['gender']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','age') || $check_field('add','age') || $check_field('set','age')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="年龄" prop="age">
												<el-input id="age" v-model="form['age']" placeholder="请输入年龄"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','age')) || (!form['student_information_id'] && $check_field('add','age'))" :disabled="disabledObj['age_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','age')">{{form['age']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','college_name') || $check_field('add','college_name') || $check_field('set','college_name')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学院名称" prop="college_name">
												<el-input id="college_name" v-model="form['college_name']" placeholder="请输入学院名称"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','college_name')) || (!form['student_information_id'] && $check_field('add','college_name'))" :disabled="disabledObj['college_name_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','college_name')">{{form['college_name']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','class_name') || $check_field('add','class_name') || $check_field('set','class_name')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="班级名称" prop="class_name">
												<el-input id="class_name" v-model="form['class_name']" placeholder="请输入班级名称"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','class_name')) || (!form['student_information_id'] && $check_field('add','class_name'))" :disabled="disabledObj['class_name_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','class_name')">{{form['class_name']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','enrollment_year') || $check_field('add','enrollment_year') || $check_field('set','enrollment_year')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="入学年份" prop="enrollment_year">
												<el-input id="enrollment_year" v-model="form['enrollment_year']" placeholder="请输入入学年份"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','enrollment_year')) || (!form['student_information_id'] && $check_field('add','enrollment_year'))" :disabled="disabledObj['enrollment_year_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','enrollment_year')">{{form['enrollment_year']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','telephone') || $check_field('add','telephone') || $check_field('set','telephone')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="电话" prop="telephone">
												<el-input id="telephone" v-model="form['telephone']" placeholder="请输入电话"
							  v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','telephone')) || (!form['student_information_id'] && $check_field('add','telephone'))" :disabled="disabledObj['telephone_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','telephone')">{{form['telephone']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','research_findings') || $check_field('add','research_findings') || $check_field('set','research_findings')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="研究成果" prop="research_findings">
								<el-input type="textarea" id="research_findings" v-model="form['research_findings']" placeholder="请输入研究成果"
						v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','research_findings')) || (!form['student_information_id'] && $check_field('add','research_findings'))" :disabled="disabledObj['research_findings_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','research_findings')">{{form['research_findings']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','research_direction') || $check_field('add','research_direction') || $check_field('set','research_direction')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="研究方向" prop="research_direction">
								<el-input type="textarea" id="research_direction" v-model="form['research_direction']" placeholder="请输入研究方向"
						v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','research_direction')) || (!form['student_information_id'] && $check_field('add','research_direction'))" :disabled="disabledObj['research_direction_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','research_direction')">{{form['research_direction']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','personal_introduction') || $check_field('add','personal_introduction') || $check_field('set','personal_introduction')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="个人简介" prop="personal_introduction">
								<el-input type="textarea" id="personal_introduction" v-model="form['personal_introduction']" placeholder="请输入个人简介"
						v-if="user_group === '管理员' || (form['student_information_id'] && $check_field('set','personal_introduction')) || (!form['student_information_id'] && $check_field('add','personal_introduction'))" :disabled="disabledObj['personal_introduction_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','personal_introduction')">{{form['personal_introduction']}}</div>
							</el-form-item>
			</el-col>
					
	
	
	
	
	
	
			<el-col :xs="24" :sm="12" :lg="8" class="el_form_btn_warp">
				<el-form-item>
					<el-button type="primary" @click="submit()">提交</el-button>
					<el-button @click="cancel()">取消</el-button>
				</el-form-item>
			</el-col>

		</el-form>
	</el-main>
</template>

<script>
	import mixin from "@/mixins/page.js";

	export default {
		mixins: [mixin],
		data() {
			return {
				field: "student_information_id",
				url_add: "~/api/student_information/add?",
				url_set: "~/api/student_information/set?",
				url_get_obj: "~/api/student_information/get_obj?",
				url_upload: "~/api/student_information/upload?",

				query: {
					"student_information_id": 0,
				},

				form: {
								"student_photos":  '', // 学生照片
										"student_account": 0, // 学生账号
										"student_name":  '', // 学生姓名
										"student_no":  '', // 学生学号
										"gender":  '', // 性别
										"age":  '', // 年龄
										"college_name":  '', // 学院名称
										"class_name":  '', // 班级名称
										"enrollment_year":  '', // 入学年份
										"telephone":  '', // 电话
										"research_findings":  '', // 研究成果
										"research_direction":  '', // 研究方向
										"personal_introduction":  '', // 个人简介
											"student_information_id": 0, // ID
						
				},
				disabledObj:{
								"student_photos_isDisabled": false,
										"student_account_isDisabled": false,
										"student_name_isDisabled": false,
										"student_no_isDisabled": false,
										"gender_isDisabled": false,
										"age_isDisabled": false,
										"college_name_isDisabled": false,
										"class_name_isDisabled": false,
										"enrollment_year_isDisabled": false,
										"telephone_isDisabled": false,
										"research_findings_isDisabled": false,
										"research_direction_isDisabled": false,
										"personal_introduction_isDisabled": false,
										},

	
		
					// 用户列表
				list_user_student_account: [],
						// 用户组
				group_user_student_account: "",
				
		
						// 性别选项列表
				list_gender: ['男','女'],
	
		
		
		
		
		
		
		
		
	
			}
		},
		methods: {


				/**
			 * 上传学生照片
			 * @param {Object} param 图片参数
			 */
			upload_student_photos(param){
						this.uploadFile(param.file, "student_photos");
					},
	
	
			
	
				/**
			 * 获取学生用户用户列表
			 */
			async get_list_user_student_account() {
                // if(this.user_group !== "管理员" && this.form["student_account"] === 0) {
                //     this.form["student_account"] = this.user.user_id;
                // }
                var json = await this.$get("~/api/user/get_list?user_group=学生用户");
                if(json.result && json.result.list){
                    this.list_user_student_account = json.result.list;
                }
                else if(json.error){
                    console.error(json.error);
                }
			},
					/**
			 * 获取学生用户用户组
			 */
			async get_group_user_student_account() {
							this.form["student_account"] = this.user.user_id;
							var json = await this.$get("~/api/user_group/get_obj?name=学生用户");
				if(json.result && json.result.obj){
					this.group_user_student_account = json.result.obj;
				}
				else if(json.error){
					console.error(json.error);
				}
			},
			get_user_session_student_account(id){
				var _this = this;
				var user_id = {"user_id":id}
				var url = "~/api/"+_this.group_user_student_account.source_table+"/get_obj?"
				this.$get(url, user_id, function(res) {
					if (res.result && res.result.obj) {
						var arr = []
						for (let key in res.result.obj) {
							arr.push(key)
						}
						var arrForm = []
									for (let key in _this.form) {
							arrForm.push(key)
						}
												_this.form["student_account"] = id
									_this.disabledObj['student_account' + '_isDisabled'] = true
						for (var i=0;i<arr.length;i++){
						  if (arr[i]!=='examine_state' && arr[i]!=='examine_reply') {
							for (var j = 0; j < arrForm.length; j++) {
							  if (arr[i] === arrForm[j]) {
								if (arr[i] !== "student_account") {
			                      _this.form[arrForm[j]] = res.result.obj[arr[i]]
			                      _this.disabledObj[arrForm[j] + '_isDisabled'] = true
								  break;
								} else {
								  _this.disabledObj[arrForm[j] + '_isDisabled'] = true
								}
							  }
							}
						  }
						}
					}
				});
			},
					get_user_student_account(id){
				var obj = this.list_user_student_account.getObj({"user_id":id});
				var ret = "";
				if(obj){
					if(obj.nickname){
						ret = obj.nickname;}
					else{
						ret = obj.username;
					}
				}
				return ret;
			},
			
	
			
	
			
	
			
	
			
	
			
	
			
	
			
	
			
	
			
	
			
	
		
			/**
			 * 获取对象之前
			 * @param {Object} param
			 */
			get_obj_before(param) {
				var form = "";
								
				if(this.form && form){
					Object.keys(this.form).forEach(key => {
						Object.keys(form).forEach(dbKey => {
							// if(dbKey === "charging_standard"){
							// 	this.form['charging_rules'] = form[dbKey];
							// 	this.disabledObj['charging_rules_isDisabled'] = true;
							// };
							if(key === dbKey){
								this.disabledObj[key+'_isDisabled'] = true;
							}
						})
					})
				}
																														$.db.del("form");
				return param;
			},

			/**
			 * 获取对象之后
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_after(json, func){


																																							


			},

			/**
			 * 提交前验证事件
			 * @param {Object} 请求参数
			 * @return {String} 验证成功返回null, 失败返回错误提示
			 */
			submit_check(param) {
				let msg = null
																																													return msg;
			},

			is_view(){
				var bl = this.user_group == "管理员";

				if(!bl){
					bl = this.$check_action('/student_information/table','add');
					console.log(bl ? "你有表格添加权限视作有添加权限" : "你没有表格添加权限");
				}
				if(!bl){
					bl = this.$check_action('/student_information/table','set');
					console.log(bl ? "你有表格添加权限视作有修改权限" : "你没有表格修改权限");
				}
				if(!bl){
					bl = this.$check_action('/student_information/view','add');
					console.log(bl ? "你有视图添加权限视作有添加权限" : "你没有视图添加权限");
				}
				if(!bl){
					bl = this.$check_action('/student_information/view','set');
					console.log(bl ? "你有视图修改权限视作有修改权限" : "你没有视图修改权限");
				}
				if(!bl){
					bl = this.$check_action('/student_information/view','get');
					console.log(bl ? "你有视图查询权限视作有查询权限" : "你没有视图查询权限");
				}

				console.log(bl ? "具有当前页面的查看权，请注意这不代表你有字段的查看权" : "无权查看当前页，请注意即便有字段查询权限没有页面查询权限也不行");

				return bl;
			},
			/**
			 * 上传文件
			 * @param {Object} param
			 */
			uploadimg(param) {
				this.uploadFile(param.file, "avatar");
			},

		},
		created() {
							this.get_list_user_student_account();
					this.get_group_user_student_account();
																											},
	}
</script>

<style>
	.avatar-uploader .el-upload {
		border: 1px dashed #d9d9d9;
		border-radius: 6px;
		cursor: pointer;
		position: relative;
		overflow: hidden;
	}

	.avatar-uploader .el-upload:hover {
		border-color: #409EFF;
	}

	.avatar-uploader-icon {
		font-size: 28px;
		color: #8c939d;
		width: 178px;
		height: 178px;
		line-height: 178px;
		text-align: center;
	}

	.avatar {
		width: 178px;
		height: 178px;
		display: block;
	}




</style>
