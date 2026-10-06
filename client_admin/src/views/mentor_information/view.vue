<template>
	<el-main class="bg edit_wrap">
		<el-form ref="form" :model="form" status-icon label-width="120px" v-if="is_view()">

							<el-col v-if="user_group === '管理员' || $check_field('get','tutor_photo') || $check_field('add','tutor_photo') || $check_field('set','tutor_photo')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师照片" prop="tutor_photo">
								<el-upload :disabled="disabledObj['tutor_photo_isDisabled']" id="tutor_photo" class="avatar-uploader" drag
						accept="image/gif, image/jpeg, image/png, image/jpg" action="" :http-request="upload_tutor_photo"
						:show-file-list="false" v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','tutor_photo')) || (!form['mentor_information_id'] && $check_field('add','tutor_photo'))">
						<img v-if="form['tutor_photo']" :src="$fullUrl(form['tutor_photo'])" class="avatar">
						<i v-else class="el-icon-plus avatar-uploader-icon"></i>
					</el-upload>
					<el-image v-else-if="$check_field('get','tutor_photo')" style="width: 100px; height: 100px"
						:src="$fullUrl(form['tutor_photo'])" :preview-src-list="[$fullUrl(form['tutor_photo'])]">
						<div slot="error" class="image-slot">
							<img src="../../../public/img/error.png" style="width: 90px; height: 90px" />
						</div>
					</el-image>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','tutor_account') || $check_field('add','tutor_account') || $check_field('set','tutor_account')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师账号" prop="tutor_account">
																		<div v-if="user_group !== '管理员'">
							{{ get_user_session_tutor_account(form['tutor_account']) }}
							<!--<el-input id="business_name" v-model="form['tutor_account']" placeholder="请输入导师账号"-->
							<!--v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','tutor_account')) || (!form['mentor_information_id'] && $check_field('add','tutor_account'))" :disabled="disabledObj['tutor_account_isDisabled']"></el-input>-->
							<!--<div v-else-if="$check_field('get','tutor_account')">{{form['tutor_account']}}</div>-->
							<el-select v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','tutor_account')) || (!form['mentor_information_id'] && $check_field('add','tutor_account'))" id="tutor_account" v-model="form['tutor_account']" :disabled="disabledObj['tutor_account_isDisabled']">
								<el-option v-for="o in list_user_tutor_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
										   :value="o['user_id']">
								</el-option>
							</el-select>
							<el-select v-else-if="$check_field('get','tutor_account')" id="tutor_account" v-model="form['tutor_account']" :disabled="true">
								<el-option v-for="o in list_user_tutor_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
										   :value="o['user_id']">
								</el-option>
							</el-select>
						</div>
						<el-select v-else id="tutor_account" v-model="form['tutor_account']" :disabled="disabledObj['tutor_account_isDisabled']">
							<el-option v-for="o in list_user_tutor_account" :key="o['username']" :label="o['nickname'] + '-' + o['username']"
									   :value="o['user_id']">
							</el-option>
						</el-select>
																</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','mentor_name') || $check_field('add','mentor_name') || $check_field('set','mentor_name')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师姓名" prop="mentor_name">
												<el-input id="mentor_name" v-model="form['mentor_name']" placeholder="请输入导师姓名"
							  v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','mentor_name')) || (!form['mentor_information_id'] && $check_field('add','mentor_name'))" :disabled="disabledObj['mentor_name_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','mentor_name')">{{form['mentor_name']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','title_of_supervisor') || $check_field('add','title_of_supervisor') || $check_field('set','title_of_supervisor')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="导师职称" prop="title_of_supervisor">
								<el-select id="title_of_supervisor" v-model="form['title_of_supervisor']"
						v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','title_of_supervisor')) || (!form['mentor_information_id'] && $check_field('add','title_of_supervisor'))">
						<el-option v-for="o in list_title_of_supervisor" :key="o" :label="o" :value="o">
						</el-option>
					</el-select>
					<div v-else-if="$check_field('get','title_of_supervisor')">{{form['title_of_supervisor']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','research_direction') || $check_field('add','research_direction') || $check_field('set','research_direction')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="研究方向" prop="research_direction">
												<el-input id="research_direction" v-model="form['research_direction']" placeholder="请输入研究方向"
							  v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','research_direction')) || (!form['mentor_information_id'] && $check_field('add','research_direction'))" :disabled="disabledObj['research_direction_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','research_direction')">{{form['research_direction']}}</div>
											</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','personal_introduction') || $check_field('add','personal_introduction') || $check_field('set','personal_introduction')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="个人介绍" prop="personal_introduction">
								<el-input type="textarea" id="personal_introduction" v-model="form['personal_introduction']" placeholder="请输入个人介绍"
						v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','personal_introduction')) || (!form['mentor_information_id'] && $check_field('add','personal_introduction'))" :disabled="disabledObj['personal_introduction_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','personal_introduction')">{{form['personal_introduction']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','enrollment_plan') || $check_field('add','enrollment_plan') || $check_field('set','enrollment_plan')" :xs="24" :sm="12" :lg="8" class="el_form_item_warp">
				<el-form-item label="招生计划" prop="enrollment_plan">
								<el-input type="textarea" id="enrollment_plan" v-model="form['enrollment_plan']" placeholder="请输入招生计划"
						v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','enrollment_plan')) || (!form['mentor_information_id'] && $check_field('add','enrollment_plan'))" :disabled="disabledObj['enrollment_plan_isDisabled']"></el-input>
					<div v-else-if="$check_field('get','enrollment_plan')">{{form['enrollment_plan']}}</div>
							</el-form-item>
			</el-col>
								<el-col v-if="user_group === '管理员' || $check_field('get','research_findings') || $check_field('add','research_findings') || $check_field('set','research_findings')" :xs="24" :sm="24" :lg="24" class="el_form_editor_warp">
				<el-form-item label="研究成果" prop="research_findings">
					<quill-editor v-model.number="form['research_findings']"
						v-if="user_group === '管理员' || (form['mentor_information_id'] && $check_field('set','research_findings')) || (!form['mentor_information_id'] && $check_field('add','research_findings')) ">
					</quill-editor>
					<div v-else-if="$check_field('get','research_findings')" v-html="form['research_findings']"></div>
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
				field: "mentor_information_id",
				url_add: "~/api/mentor_information/add?",
				url_set: "~/api/mentor_information/set?",
				url_get_obj: "~/api/mentor_information/get_obj?",
				url_upload: "~/api/mentor_information/upload?",

				query: {
					"mentor_information_id": 0,
				},

				form: {
								"tutor_photo":  '', // 导师照片
										"tutor_account": 0, // 导师账号
										"mentor_name":  '', // 导师姓名
										"title_of_supervisor":  '', // 导师职称
										"research_direction":  '', // 研究方向
										"personal_introduction":  '', // 个人介绍
										"enrollment_plan":  '', // 招生计划
										"research_findings":  '', // 研究成果
											"mentor_information_id": 0, // ID
						
				},
				disabledObj:{
								"tutor_photo_isDisabled": false,
										"tutor_account_isDisabled": false,
										"mentor_name_isDisabled": false,
										"title_of_supervisor_isDisabled": false,
										"research_direction_isDisabled": false,
										"personal_introduction_isDisabled": false,
										"enrollment_plan_isDisabled": false,
										"research_findings_isDisabled": false,
										},

	
		
					// 用户列表
				list_user_tutor_account: [],
						// 用户组
				group_user_tutor_account: "",
				
						// 导师职称选项列表
				list_title_of_supervisor: ['助教','讲师','副教授','教授'],
	
		
		
		
		
	
			}
		},
		methods: {


				/**
			 * 上传导师照片
			 * @param {Object} param 图片参数
			 */
			upload_tutor_photo(param){
						this.uploadFile(param.file, "tutor_photo");
					},
	
	
			
	
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
					/**
			 * 获取导师用户用户组
			 */
			async get_group_user_tutor_account() {
							this.form["tutor_account"] = this.user.user_id;
							var json = await this.$get("~/api/user_group/get_obj?name=导师用户");
				if(json.result && json.result.obj){
					this.group_user_tutor_account = json.result.obj;
				}
				else if(json.error){
					console.error(json.error);
				}
			},
			get_user_session_tutor_account(id){
				var _this = this;
				var user_id = {"user_id":id}
				var url = "~/api/"+_this.group_user_tutor_account.source_table+"/get_obj?"
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
												_this.form["tutor_account"] = id
									_this.disabledObj['tutor_account' + '_isDisabled'] = true
						for (var i=0;i<arr.length;i++){
						  if (arr[i]!=='examine_state' && arr[i]!=='examine_reply') {
							for (var j = 0; j < arrForm.length; j++) {
							  if (arr[i] === arrForm[j]) {
								if (arr[i] !== "tutor_account") {
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
					bl = this.$check_action('/mentor_information/table','add');
					console.log(bl ? "你有表格添加权限视作有添加权限" : "你没有表格添加权限");
				}
				if(!bl){
					bl = this.$check_action('/mentor_information/table','set');
					console.log(bl ? "你有表格添加权限视作有修改权限" : "你没有表格修改权限");
				}
				if(!bl){
					bl = this.$check_action('/mentor_information/view','add');
					console.log(bl ? "你有视图添加权限视作有添加权限" : "你没有视图添加权限");
				}
				if(!bl){
					bl = this.$check_action('/mentor_information/view','set');
					console.log(bl ? "你有视图修改权限视作有修改权限" : "你没有视图修改权限");
				}
				if(!bl){
					bl = this.$check_action('/mentor_information/view','get');
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
					this.get_group_user_tutor_account();
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
