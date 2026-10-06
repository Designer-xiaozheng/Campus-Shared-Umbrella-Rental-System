<template>
	<el-main class="bg edit_wrap">
		<el-form ref="form" :model="form" status-icon label-width="120px" v-if="is_view()">

							<el-col v-if="user_group === '管理员' || $check_field('get','tutor_account') || $check_field('add','tutor_account') || $check_field('set','tutor_account')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师账号" prop="tutor_account">
													<el-select v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','tutor_account')) || (!form['application_for_registration_id'] && $check_field('add','tutor_account'))" id="tutor_account" v-model="form['tutor_account']" :disabled="disabledObj['tutor_account_isDisabled']">
							<el-option v-for="o in list_user_tutor_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
									   :value="o['user_id']">
							</el-option>
						</el-select>
						<el-select v-else-if="$check_field('get','tutor_account')" id="tutor_account" v-model="form['tutor_account']" :disabled="true">
							<el-option v-for="o in list_user_tutor_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
									   :value="o['user_id']">
							</el-option>
						</el-select>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','mentor_name') || $check_field('add','mentor_name') || $check_field('set','mentor_name')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师姓名" prop="mentor_name">
												<el-input id="mentor_name" v-model="form['mentor_name']" placeholder="请输入导师姓名"
							  v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','mentor_name')) || (!form['application_for_registration_id'] && $check_field('add','mentor_name'))" :disabled="disabledObj['mentor_name_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','mentor_name')">{{form['mentor_name']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','title_of_supervisor') || $check_field('add','title_of_supervisor') || $check_field('set','title_of_supervisor')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师职称" prop="title_of_supervisor">
												<el-input id="title_of_supervisor" v-model="form['title_of_supervisor']" placeholder="请输入导师职称"
							  v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','title_of_supervisor')) || (!form['application_for_registration_id'] && $check_field('add','title_of_supervisor'))" :disabled="disabledObj['title_of_supervisor_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','title_of_supervisor')">{{form['title_of_supervisor']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_account') || $check_field('add','student_account') || $check_field('set','student_account')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生账号" prop="student_account">
																		<div v-if="user_group !== '管理员'">
							{{ get_user_session_student_account(form['student_account']) }}
							<!--<el-input id="business_name" v-model="form['student_account']" placeholder="请输入学生账号"-->
							<!--v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','student_account')) || (!form['application_for_registration_id'] && $check_field('add','student_account'))" :disabled="disabledObj['student_account_isDisabled']"></el-input>-->
							<!--<div v-else-if="$check_field('get','student_account')">{{form['student_account']}}</div>-->
							<el-select v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','student_account')) || (!form['application_for_registration_id'] && $check_field('add','student_account'))" id="student_account" v-model="form['student_account']" :disabled="disabledObj['student_account_isDisabled']">
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
							  v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','student_name')) || (!form['application_for_registration_id'] && $check_field('add','student_name'))" :disabled="disabledObj['student_name_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','student_name')">{{form['student_name']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','telephone') || $check_field('add','telephone') || $check_field('set','telephone')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="电话" prop="telephone">
												<el-input id="telephone" v-model="form['telephone']" placeholder="请输入电话"
							  v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','telephone')) || (!form['application_for_registration_id'] && $check_field('add','telephone'))" :disabled="disabledObj['telephone_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','telephone')">{{form['telephone']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','resume') || $check_field('add','resume') || $check_field('set','resume')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="简历" prop="resume">
												<div v-if="disabledObj['resume_isDisabled']">
						<div v-if="$check_field('get','resume')">
							<el-button type="primary" @click="$download($fullUrl(form['resume']),form['resume'])">下载<i
									class="el-icon-download el-icon--right"></i></el-button>
						</div>
					</div>
					<div v-else>
						<el-upload v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','resume')) || (!form['application_for_registration_id'] && $check_field('add','resume'))" class="upload-demo" drag
								   action="" style="max-width: 300px;width: 100%;" :http-request="upload_resume" :limit="1" accept="">
							<i class="el-icon-upload"></i>
							<div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
						</el-upload>
						<div v-else-if="$check_field('get','resume')">
							<el-button type="primary" @click="$download($fullUrl(form['resume']),form['resume'])">下载<i
									class="el-icon-download el-icon--right"></i></el-button>
						</div>
					</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_research_direction') || $check_field('add','student_research_direction') || $check_field('set','student_research_direction')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生研究方向" prop="student_research_direction">
												<el-input id="student_research_direction" v-model="form['student_research_direction']" placeholder="请输入学生研究方向"
							  v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','student_research_direction')) || (!form['application_for_registration_id'] && $check_field('add','student_research_direction'))" :disabled="disabledObj['student_research_direction_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','student_research_direction')">{{form['student_research_direction']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_research_results') || $check_field('add','student_research_results') || $check_field('set','student_research_results')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="学生研究成果" prop="student_research_results">
								<el-input type="textarea" id="student_research_results" v-model="form['student_research_results']" placeholder="请输入学生研究成果"
						v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','student_research_results')) || (!form['application_for_registration_id'] && $check_field('add','student_research_results'))" :disabled="disabledObj['student_research_results_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','student_research_results')">{{form['student_research_results']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','student_introduction') || $check_field('add','student_introduction') || $check_field('set','student_introduction')" :xs="24" :sm="24" :lg="24" class="el_form_editor_warp">
				<el-form-item label="学生简介" prop="student_introduction">
					<quill-editor v-model.number="form['student_introduction']"
						v-if="user_group === '管理员' || (form['application_for_registration_id'] && $check_field('set','student_introduction')) || (!form['application_for_registration_id'] && $check_field('add','student_introduction')) ">
					</quill-editor>
					<div v-else-if="$check_field('get','student_introduction')" v-html="form['student_introduction']"></div>
				</el-form-item>
			</el-col>
							<el-col :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="审核状态" prop="examine_state">
					<el-select id="examine_state" v-model="form['examine_state']"
						v-if="user_group === '管理员' || (form['examine_state'] && $check_examine()) || (!form['examine_state'] && $check_examine())">
						<el-option key="未审核" label="未审核" value="未审核"></el-option>
						<el-option key="已通过" label="已通过" value="已通过"></el-option>
						<el-option key="未通过" label="未通过" value="未通过"></el-option>
					</el-select>
					<div v-else>{{form["examine_state"]}}</div>
				</el-form-item>
			</el-col>
					<el-col :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="审核回复" prop="examine_reply">
					<el-input id="examine_reply" v-model="form['examine_reply']" placeholder="请输入审核回复"
						v-if="user_group === '管理员' || (form['examine_reply'] && $check_examine()) || (!form['examine_reply'] && $check_examine())"></el-input>
					<div v-else>{{form["examine_reply"]}}</div>
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
				field: "application_for_registration_id",
				url_add: "~/api/application_for_registration/add?",
				url_set: "~/api/application_for_registration/set?",
				url_get_obj: "~/api/application_for_registration/get_obj?",
				url_upload: "~/api/application_for_registration/upload?",

				query: {
					"application_for_registration_id": 0,
				},

				form: {
								"tutor_account": 0, // 导师账号
										"mentor_name":  '', // 导师姓名
										"title_of_supervisor":  '', // 导师职称
										"student_account": 0, // 学生账号
										"student_name":  '', // 学生姓名
										"telephone":  '', // 电话
										"resume":  '', // 简历
										"student_research_direction":  '', // 学生研究方向
										"student_research_results":  '', // 学生研究成果
										"student_introduction":  '', // 学生简介
									"examine_state": "未审核",
							"examine_reply": "",
							"application_for_registration_id": 0, // ID
						
				},
				disabledObj:{
								"tutor_account_isDisabled": false,
										"mentor_name_isDisabled": false,
										"title_of_supervisor_isDisabled": false,
										"student_account_isDisabled": false,
										"student_name_isDisabled": false,
										"telephone_isDisabled": false,
										"resume_isDisabled": false,
										"student_research_direction_isDisabled": false,
										"student_research_results_isDisabled": false,
										"student_introduction_isDisabled": false,
										},

	
					// 用户列表
				list_user_tutor_account: [],
				
		
		
					// 用户列表
				list_user_student_account: [],
						// 用户组
				group_user_student_account: "",
				
		
		
		
		
		
	
			}
		},
		methods: {


	
	
				/**
			 * 获取导师用户用户列表
			 */
			async get_list_user_tutor_account() {
                // if(this.user_group !== "管理员" && this.form["tutor_account"] === 0) {
                //     this.form["tutor_account"] = this.user.user_id;
                // }
                var json = await this.$get("~/api/user/get_list?user_group=导师用户");
                if(json.result && json.result.list){
                    this.list_user_tutor_account = json.result.list;
                }
                else if(json.error){
                    console.error(json.error);
                }
			},
					get_user_tutor_account(id){
				var obj = this.list_user_tutor_account.getObj({"user_id":id});
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
			 * 上传简历
			 * @param {Object} param 文件参数
			 */
			upload_resume(param){
						this.uploadFile(param.file, "resume");
					},
	
	
			
	
			
	
			
	
		
			/**
			 * 获取对象之前
			 * @param {Object} param
			 */
			get_obj_before(param) {
				var form = "";
										// 获取缓存数据附加
				form = $.db.get("form");
							$.push(this.form ,form);
							
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
					bl = this.$check_action('/application_for_registration/table','add');
					console.log(bl ? "你有表格添加权限视作有添加权限" : "你没有表格添加权限");
				}
				if(!bl){
					bl = this.$check_action('/application_for_registration/table','set');
					console.log(bl ? "你有表格添加权限视作有修改权限" : "你没有表格修改权限");
				}
				if(!bl){
					bl = this.$check_action('/application_for_registration/view','add');
					console.log(bl ? "你有视图添加权限视作有添加权限" : "你没有视图添加权限");
				}
				if(!bl){
					bl = this.$check_action('/application_for_registration/view','set');
					console.log(bl ? "你有视图修改权限视作有修改权限" : "你没有视图修改权限");
				}
				if(!bl){
					bl = this.$check_action('/application_for_registration/view','get');
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
					this.get_list_user_tutor_account();
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
