<template>
	<div class="diy_edit page_application_for_registration" id="application_for_registration_edit">
		<div class='warp'>
			<div class='container'>
				<div class='row diy_edit_content_box'>
						<div v-if="$check_field('set','tutor_account') || $check_field('add','tutor_account') || $check_field('get','tutor_account')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								导师账号:
							</span>
						</div>
						<div class="diy_field diy_down">
							<select id="form_tutor_account" :disabled="disabledObj['tutor_account_isDisabled']" v-model="form['tutor_account']" v-if="(form['tutor_account'] && $check_field('set','tutor_account')) || (!form['tutor_account'] && $check_field('add','tutor_account'))" >
								<option v-for="o in list_user_tutor_account" :value="o['user_id']">
									{{o['nickname'] + '-' + o['username']}}
								</option>
							</select>
							<span v-else-if="$check_field('get','tutor_account')">{{ form['tutor_account'] }}</span>
						</div>
					</div>
							<div v-if="$check_field('set','mentor_name') || $check_field('add','mentor_name') || $check_field('get','mentor_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								导师姓名:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_mentor_name" v-model="form['mentor_name']" placeholder="请输入导师姓名" v-if="(form['mentor_name'] && $check_field('set','mentor_name')) || (!form['mentor_name'] && $check_field('add','mentor_name'))"  :disabled="disabledObj['mentor_name_isDisabled']"/>
							<span v-else-if="$check_field('get','mentor_name')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','title_of_supervisor') || $check_field('add','title_of_supervisor') || $check_field('get','title_of_supervisor')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								导师职称:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_title_of_supervisor" v-model="form['title_of_supervisor']" placeholder="请输入导师职称" v-if="(form['title_of_supervisor'] && $check_field('set','title_of_supervisor')) || (!form['title_of_supervisor'] && $check_field('add','title_of_supervisor'))"  :disabled="disabledObj['title_of_supervisor_isDisabled']"/>
							<span v-else-if="$check_field('get','title_of_supervisor')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','student_account') || $check_field('add','student_account') || $check_field('get','student_account')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生账号:
							</span>
						</div>
						<div class="diy_field diy_down">
							<select id="form_student_account" :disabled="disabledObj['student_account_isDisabled']" v-model="form['student_account']" v-if="(form['student_account'] && $check_field('set','student_account')) || (!form['student_account'] && $check_field('add','student_account'))" >
								<option v-for="o in list_user_student_account" :value="o['user_id']">
									{{o['nickname'] + '-' + o['username']}}
								</option>
							</select>
							<span v-else-if="$check_field('get','student_account')">{{ form['student_account'] }}</span>
						</div>
					</div>
							<div v-if="$check_field('set','student_name') || $check_field('add','student_name') || $check_field('get','student_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生姓名:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_student_name" v-model="form['student_name']" placeholder="请输入学生姓名" v-if="(form['student_name'] && $check_field('set','student_name')) || (!form['student_name'] && $check_field('add','student_name'))"  :disabled="disabledObj['student_name_isDisabled']"/>
							<span v-else-if="$check_field('get','student_name')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','telephone') || $check_field('add','telephone') || $check_field('get','telephone')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								电话:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_telephone" v-model="form['telephone']" placeholder="请输入电话" v-if="(form['telephone'] && $check_field('set','telephone')) || (!form['telephone'] && $check_field('add','telephone'))"  :disabled="disabledObj['telephone_isDisabled']"/>
							<span v-else-if="$check_field('get','telephone')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','resume') || $check_field('add','resume') || $check_field('get','resume')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								简历:
							</span>
						</div>
								<!-- 文件 -->
						<input type="file" style="display: none;" id="form_file_resume" title="resume" @change="change_file($event.target.files,'resume')"/>
						<!-- 修改权限 -->
						<div class="diy_field diy_img" v-if="form['resume'] && $check_field('set','resume')">
							<label for="form_file_resume">
								<!--<span>{{form['resume']}} </span>-->
								<a :href="$fullUrl(form['resume'])" target="_blank" style="color: rgb(64, 158, 255);">点击下载</a>
							</label>
						</div>
						<!-- 添加权限 -->
						<div class="diy_field diy_img" v-else-if="!form['resume'] && $check_field('add','resume')">
							<label for="form_file_resume">
								<div class="btn_add_img">
									<span>+</span>
								</div>
							</label>
						</div>
						<!-- 查询权限 -->
						<div class="diy_field diy_img" v-else-if="$check_field('get','resume')">
							<span>{{form['resume']}} </span>
						</div>
							</div>
							<div v-if="$check_field('set','student_research_direction') || $check_field('add','student_research_direction') || $check_field('get','student_research_direction')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生研究方向:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_student_research_direction" v-model="form['student_research_direction']" placeholder="请输入学生研究方向" v-if="(form['student_research_direction'] && $check_field('set','student_research_direction')) || (!form['student_research_direction'] && $check_field('add','student_research_direction'))"  :disabled="disabledObj['student_research_direction_isDisabled']"/>
							<span v-else-if="$check_field('get','student_research_direction')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','student_research_results') || $check_field('add','student_research_results') || $check_field('get','student_research_results')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生研究成果:
							</span>
						</div>
								<!-- 多文本 -->
						<div class="diy_field diy_desc">
							<textarea id="form_student_research_results" v-model="form['student_research_results']" v-if="(form['student_research_results'] && $check_field('set','student_research_results')) || (!form['student_research_results'] && $check_field('add','student_research_results'))" :disabled="disabledObj['student_research_results_isDisabled']" />
							<span v-else-if="$check_field('get','student_research_results')">{{ form['${obj.name}'] }}</span>
						</div>
							</div>
							<div v-if="$check_field('set','student_introduction') || $check_field('add','student_introduction') || $check_field('get','student_introduction')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生简介:
							</span>
						</div>
								<!-- 多文本 -->
						<div class="diy_field diy_desc">
							<textarea id="form_student_introduction" v-model="form['student_introduction']" v-if="(form['student_introduction'] && $check_field('set','student_introduction')) || (!form['student_introduction'] && $check_field('add','student_introduction'))"  :disabled="disabledObj['student_introduction_isDisabled']"/>
							<view v-else-if="$check_field('get','student_introduction')" v-html="form['${obj.name}']"></view>
						</div>
							</div>
	


					<div v-if="user_group === '管理员' || $check_examine()" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								审核状态:
							</span>
						</div>
						<div class="diy_field diy_select" v-if="$check_action('/application_for_registration/edit','examine')">
							<!--<span> {{ form['examine_state'] }} </span>-->
							<select v-model="form['examine_state']">
								<option value="未审核">
									未审核
								</option>
								<option value="已通过">
									已通过
								</option>
								<option value="未通过">
									未通过
								</option>
							</select>
						</div>
						<div class="diy_field diy_text" v-else>
							<span>
								{{ form['examine_state'] }}
							</span>
						</div>
					</div>
					<div v-if="user_group === '管理员' || $check_examine()" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								审核回复:
							</span>
						</div>
						<div class="diy_field diy_desc" v-if="$check_action('/application_for_registration/edit','examine')">
							<textarea v-model="form['examine_reply']"></textarea>
						</div>
						<div class="diy_field diy_text" v-else>
							<span>
								{{ form['examine_reply'] }}
							</span>
						</div>
					</div>


				</div>
				<div class="diy_edit_submit_box row">
					<div class="col-12">
						<div class="btn_box">
							<button class="btn_submit" @click="submit()">提交</button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import mixin from "@/mixins/page.js";
	export default {
		mixins: [mixin],
		components: {},
		data() {
			return {
				url_get_obj: "~/api/application_for_registration/get_obj?",
				url_add: "~/api/application_for_registration/add?",
				url_set: "~/api/application_for_registration/set?",

				// 登录权限
				oauth: {
					"signIn": true,
					"user_group": []
				},

				// 查询条件
				query: {
						"tutor_account": 0,
							"mentor_name": "",
							"title_of_supervisor": "",
							"student_account": 0,
							"student_name": "",
							"telephone": "",
							"resume": "",
							"student_research_direction": "",
							"student_research_results": "",
							"student_introduction": "",
						"application_for_registration_id": 0,
				},

				obj: {
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
					"application_for_registration_id": 0,
				},

				// 表单字段
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
					"application_for_registration_id": 0,
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
													
				// ID字段
				field: "application_for_registration_id",

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
					async get_user_session_student_account(){
				var _this = this;
				var json = await this.$get("~/api/user_group/get_obj?name=学生用户");
				if(json.result && json.result.obj){
					var source_table = json.result.obj.source_table;
					var user_id = _this.$store.state.user.user_id;
					if (user_id){
						var url = "~/api/"+source_table+"/get_obj?"
						this.$get(url, {"user_id":_this.$store.state.user.user_id}, function(res) {
							if (res.result && res.result.obj) {
								var arr = []
								for (let key in res.result.obj) {
									arr.push(key)
								}
								var arrForm = []
								for (let key in _this.form) {
									arrForm.push(key)
								}
								_this.form["student_account"] = user_id
								_this.disabledObj['student_account' + '_isDisabled'] = true
								for (var i=0;i<arr.length;i++){
                  if (arr[i]!=='examine_state' && arr[i]!=='examine_reply') {
                    for (var j = 0; j < arrForm.length; j++) {
                      if (arr[i] === arrForm[j]) {
                        if (arr[i] !== "student_account") {
                          _this.form[arrForm[j]] = res.result.obj[arr[i]]
                          _this.disabledObj[arrForm[j] + '_isDisabled'] = true
                          break;
                        }
                      }
                    }
                  }
								}
							}
						});
					}
				}
				else if(json.error){
					console.error(json.error);
				}
			},
	
				
				
				
				
				
				
	
			/**
			 * 修改文件
			 * @param { Object } files 上传文件对象
			 * @param { String } str 表单的属性名
			 */
			change_file(files, str) {
				var form = new FormData();
				form.append("file", files[0]);
				this.$post("~/api/application_for_registration/upload?", form, (res) => {
					if (res.result) {
						this.form[str] = res.result.url;
					} else if (res.error) {
						this.$toast(res.error.message);
					}
				});
			},

			/**
			 * 获取对象后获取缓存表单
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_before(param){
				var form = $.db.get("form");
				// if (form) {
        //   delete(form.examine_state)
        //   delete(form.examine_reply)
        //   this.obj = $.push(this.obj ,form);
				// 	this.form = $.push(this.form ,form);
				// }
				// var arr = []
				// for (let key in form) {
				// 	arr.push(key)
				// }
				// for (var i=0;i<arr.length;i++){
				// 	this.disabledObj[arr[i] + '_isDisabled'] = true
				// }
        if (form) {
          var arr = []
          for (let key in form) {
            arr.push(key)
          }
          var arrForm = []
          for (let key in this.form) {
            arrForm.push(key)
          }
          for (var i=0;i<arr.length;i++){
            if (arr[i]!=='examine_state' && arr[i]!=='examine_reply') {
              for (var j = 0; j < arrForm.length; j++) {
                if (arrForm[j] === arr[i]) {
                  this.form[arrForm[j]] = form[arr[i]]
                  this.obj[arrForm[j]] = form[arr[i]]
                  this.disabledObj[arrForm[j] + '_isDisabled'] = true
                  break;
                }
              }
            }
          }
        }
																				
        $.db.del("form");
				return param;
			},

			/**
			 * 获取对象后获取缓存表单
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_after(json ,func){
				// var form = $.db.get("form");
				// var obj = Object.assign({} ,form ,this.obj);
				// if (obj) {
        //   delete(obj.examine_state)
        //   delete(obj.examine_reply)
				// 	this.obj = $.push(this.obj ,obj);
				// }
				// if (form) {
        //   delete(form.examine_state)
        //   delete(form.examine_reply)
				// 	this.form = $.push(this.form ,form);
				// }

				if(func){
					func(json);
				}
			},

		},
		created() {
						this.get_list_user_tutor_account();
												this.get_user_session_student_account();
					this.get_list_user_student_account();
																					},
	}
</script>

<style>




</style>
