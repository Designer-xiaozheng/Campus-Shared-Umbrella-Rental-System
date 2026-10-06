<template>
	<div class="diy_edit page_student_information" id="student_information_edit">
		<div class='warp'>
			<div class='container'>
				<div class='row diy_edit_content_box'>
						<div v-if="$check_field('set','student_photos') || $check_field('add','student_photos') || $check_field('get','student_photos')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生照片:
							</span>
						</div>
								<!-- 图片 -->
						<input type="file" :disabled="disabledObj['student_photos_isDisabled']" style="display: none;" id="form_img_student_photos" title="student_photos" @change="change_file($event.target.files,'student_photos')"/>
						<!-- 修改权限 -->
						<div class="diy_field diy_img" v-if="form['student_photos'] && $check_field('set','student_photos')">
							<label for="form_img_student_photos">
								<img :src="$fullUrl(form['student_photos'])" />
							</label>
						</div>
						<!-- 添加权限 -->
						<div class="diy_field diy_img" v-else-if="!form['student_photos'] && $check_field('add','student_photos')">
							<label for="form_img_student_photos">
								<div class="btn_add_img">
									<span>+</span>
								</div>
							</label>
						</div>
						<!-- 查询权限 -->
						<div class="diy_field diy_img" v-else-if="$check_field('get','student_photos')">
							<img :src="$fullUrl(form['student_photos'])" />
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
							<div v-if="$check_field('set','student_no') || $check_field('add','student_no') || $check_field('get','student_no')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学生学号:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_student_no" v-model="form['student_no']" placeholder="请输入学生学号" v-if="(form['student_no'] && $check_field('set','student_no')) || (!form['student_no'] && $check_field('add','student_no'))"  :disabled="disabledObj['student_no_isDisabled']"/>
							<span v-else-if="$check_field('get','student_no')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','gender') || $check_field('add','gender') || $check_field('get','gender')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								性别:
							</span>
						</div>
								<!-- 选项 -->
						<div class="diy_field diy_down">
							<select id="form_gender" v-model="form['gender']" v-if="(form['gender'] && $check_field('set','gender')) || (!form['gender'] && $check_field('add','gender'))" >
								<option v-for="o in list_gender" :value="o">
									{{o}}
								</option>
							</select>
							<span v-else-if="$check_field('get','gender')">{{ form['gender'] }}</span>
						</div>
							</div>
							<div v-if="$check_field('set','age') || $check_field('add','age') || $check_field('get','age')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								年龄:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_age" v-model="form['age']" placeholder="请输入年龄" v-if="(form['age'] && $check_field('set','age')) || (!form['age'] && $check_field('add','age'))"  :disabled="disabledObj['age_isDisabled']"/>
							<span v-else-if="$check_field('get','age')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','college_name') || $check_field('add','college_name') || $check_field('get','college_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学院名称:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_college_name" v-model="form['college_name']" placeholder="请输入学院名称" v-if="(form['college_name'] && $check_field('set','college_name')) || (!form['college_name'] && $check_field('add','college_name'))"  :disabled="disabledObj['college_name_isDisabled']"/>
							<span v-else-if="$check_field('get','college_name')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','class_name') || $check_field('add','class_name') || $check_field('get','class_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								班级名称:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_class_name" v-model="form['class_name']" placeholder="请输入班级名称" v-if="(form['class_name'] && $check_field('set','class_name')) || (!form['class_name'] && $check_field('add','class_name'))"  :disabled="disabledObj['class_name_isDisabled']"/>
							<span v-else-if="$check_field('get','class_name')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','enrollment_year') || $check_field('add','enrollment_year') || $check_field('get','enrollment_year')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								入学年份:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_enrollment_year" v-model="form['enrollment_year']" placeholder="请输入入学年份" v-if="(form['enrollment_year'] && $check_field('set','enrollment_year')) || (!form['enrollment_year'] && $check_field('add','enrollment_year'))"  :disabled="disabledObj['enrollment_year_isDisabled']"/>
							<span v-else-if="$check_field('get','enrollment_year')">{{ form['${obj.name}'] }}</span>
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
							<div v-if="$check_field('set','research_findings') || $check_field('add','research_findings') || $check_field('get','research_findings')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								研究成果:
							</span>
						</div>
								<!-- 多文本 -->
						<div class="diy_field diy_desc">
							<textarea id="form_research_findings" v-model="form['research_findings']" v-if="(form['research_findings'] && $check_field('set','research_findings')) || (!form['research_findings'] && $check_field('add','research_findings'))" :disabled="disabledObj['research_findings_isDisabled']" />
							<span v-else-if="$check_field('get','research_findings')">{{ form['${obj.name}'] }}</span>
						</div>
							</div>
							<div v-if="$check_field('set','research_direction') || $check_field('add','research_direction') || $check_field('get','research_direction')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								研究方向:
							</span>
						</div>
								<!-- 多文本 -->
						<div class="diy_field diy_desc">
							<textarea id="form_research_direction" v-model="form['research_direction']" v-if="(form['research_direction'] && $check_field('set','research_direction')) || (!form['research_direction'] && $check_field('add','research_direction'))" :disabled="disabledObj['research_direction_isDisabled']" />
							<span v-else-if="$check_field('get','research_direction')">{{ form['${obj.name}'] }}</span>
						</div>
							</div>
							<div v-if="$check_field('set','personal_introduction') || $check_field('add','personal_introduction') || $check_field('get','personal_introduction')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								个人简介:
							</span>
						</div>
								<!-- 多文本 -->
						<div class="diy_field diy_desc">
							<textarea id="form_personal_introduction" v-model="form['personal_introduction']" v-if="(form['personal_introduction'] && $check_field('set','personal_introduction')) || (!form['personal_introduction'] && $check_field('add','personal_introduction'))" :disabled="disabledObj['personal_introduction_isDisabled']" />
							<span v-else-if="$check_field('get','personal_introduction')">{{ form['${obj.name}'] }}</span>
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
				url_get_obj: "~/api/student_information/get_obj?",
				url_add: "~/api/student_information/add?",
				url_set: "~/api/student_information/set?",

				// 登录权限
				oauth: {
					"signIn": true,
					"user_group": []
				},

				// 查询条件
				query: {
						"student_photos": "",
							"student_account": 0,
							"student_name": "",
							"student_no": "",
							"gender": "",
							"age": "",
							"college_name": "",
							"class_name": "",
							"enrollment_year": "",
							"telephone": "",
							"research_findings": "",
							"research_direction": "",
							"personal_introduction": "",
						"student_information_id": 0,
				},

				obj: {
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
						"student_information_id": 0,
				},

				// 表单字段
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
						"student_information_id": 0,
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
										// 性别选项列表
				list_gender: ['男','女'],
																		
				// ID字段
				field: "student_information_id",

			}
		},
		methods: {
			
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
				this.$post("~/api/student_information/upload?", form, (res) => {
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
								this.get_user_session_student_account();
					this.get_list_user_student_account();
																																				},
	}
</script>

<style>




</style>
