<template>
  <div class="page_search">
	<div class="warp">
	  <div class="container">
		<div class="row">
		  <div class="col-12">
			<div class="card_result_search">
			  <div class="title">搜索结果</div>

				<!-- 文章搜索结果 -->
			  <list_result_search
				:list="result_article"
				title="学校资讯"
				source_table="article"
			  ></list_result_search>


						  <list_result_search
				v-if="$check_action('/student_users/list', 'get')"
				:list="result_student_users_student_account"
				title="学生用户学生账号"
				source_table="student_users"
			  ></list_result_search>
											  <list_result_search
				v-if="$check_action('/student_users/list', 'get')"
				:list="result_student_users_college_name"
				title="学生用户学院名称"
				source_table="student_users"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/student_users/list', 'get')"
				:list="result_student_users_class_name"
				title="学生用户班级名称"
				source_table="student_users"
			  ></list_result_search>
									  <list_result_search
				v-if="$check_action('/mentor_user/list', 'get')"
				:list="result_mentor_user_tutor_account"
				title="导师用户导师账号"
				source_table="mentor_user"
			  ></list_result_search>
																		  <list_result_search
				v-if="$check_action('/student_information/list', 'get')"
				:list="result_student_information_student_name"
				title="学生信息学生姓名"
				source_table="student_information"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/student_information/list', 'get')"
				:list="result_student_information_student_no"
				title="学生信息学生学号"
				source_table="student_information"
			  ></list_result_search>
														  <list_result_search
				v-if="$check_action('/student_information/list', 'get')"
				:list="result_student_information_college_name"
				title="学生信息学院名称"
				source_table="student_information"
			  ></list_result_search>
																																	  <list_result_search
				v-if="$check_action('/mentor_information/list', 'get')"
				:list="result_mentor_information_mentor_name"
				title="导师信息导师姓名"
				source_table="mentor_information"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/mentor_information/list', 'get')"
				:list="result_mentor_information_title_of_supervisor"
				title="导师信息导师职称"
				source_table="mentor_information"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/mentor_information/list', 'get')"
				:list="result_mentor_information_research_direction"
				title="导师信息研究方向"
				source_table="mentor_information"
			  ></list_result_search>
																														  <list_result_search
				v-if="$check_action('/application_for_registration/list', 'get')"
				:list="result_application_for_registration_student_name"
				title="报名申请学生姓名"
				source_table="application_for_registration"
			  ></list_result_search>
																					</div>
		  </div>
		</div>
	  </div>
	</div>
  </div>
</template>

<script>
import mixin from "../../mixins/page.js";
import list_result_search from "../../components/diy/list_result_search.vue";

export default {
  mixins: [mixin],
  data() {
	return {
	  "query": {
		word: "",
	  },
	  "result_article": [],
						"result_student_users_student_account":[],
											"result_student_users_college_name":[],
								"result_student_users_class_name":[],
									"result_mentor_user_tutor_account":[],
																		"result_student_information_student_name":[],
								"result_student_information_student_no":[],
														"result_student_information_college_name":[],
																																	"result_mentor_information_mentor_name":[],
								"result_mentor_information_title_of_supervisor":[],
								"result_mentor_information_research_direction":[],
																														"result_application_for_registration_student_name":[],
																			};
  },
  methods: {
	/**
	 * 获取文章
	 */
	get_article() {
	  this.$get("~/api/article/get_list?like=0", { page: 1, size: 10, title: this.query.word }, (json) => {
		if (json.result) {
		  this.result_article = json.result.list;
		}
	  });
	},

				/**
	 * 获取student_account
	 */
	get_student_users_student_account(){
		let url = "~/api/student_users/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "student_account": this.query.word }, (json) => {
		  if (json.result) {
			var result_student_users_student_account = json.result.list;
			result_student_users_student_account.map(o => o.title = o['student_account'])
	  			this.result_student_users_student_account = result_student_users_student_account
		 	}
		});
	},
									/**
	 * 获取college_name
	 */
	get_student_users_college_name(){
		let url = "~/api/student_users/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "college_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_student_users_college_name = json.result.list;
			result_student_users_college_name.map(o => o.title = o['college_name'])
	  			this.result_student_users_college_name = result_student_users_college_name
		 	}
		});
	},
						/**
	 * 获取class_name
	 */
	get_student_users_class_name(){
		let url = "~/api/student_users/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "class_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_student_users_class_name = json.result.list;
			result_student_users_class_name.map(o => o.title = o['class_name'])
	  			this.result_student_users_class_name = result_student_users_class_name
		 	}
		});
	},
							/**
	 * 获取tutor_account
	 */
	get_mentor_user_tutor_account(){
		let url = "~/api/mentor_user/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "tutor_account": this.query.word }, (json) => {
		  if (json.result) {
			var result_mentor_user_tutor_account = json.result.list;
			result_mentor_user_tutor_account.map(o => o.title = o['tutor_account'])
	  			this.result_mentor_user_tutor_account = result_mentor_user_tutor_account
		 	}
		});
	},
																/**
	 * 获取student_name
	 */
	get_student_information_student_name(){
		let url = "~/api/student_information/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "student_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_student_information_student_name = json.result.list;
			result_student_information_student_name.map(o => o.title = o['student_name'])
	  			this.result_student_information_student_name = result_student_information_student_name
		 	}
		});
	},
						/**
	 * 获取student_no
	 */
	get_student_information_student_no(){
		let url = "~/api/student_information/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "student_no": this.query.word }, (json) => {
		  if (json.result) {
			var result_student_information_student_no = json.result.list;
			result_student_information_student_no.map(o => o.title = o['student_no'])
	  			this.result_student_information_student_no = result_student_information_student_no
		 	}
		});
	},
												/**
	 * 获取college_name
	 */
	get_student_information_college_name(){
		let url = "~/api/student_information/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "college_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_student_information_college_name = json.result.list;
			result_student_information_college_name.map(o => o.title = o['college_name'])
	  			this.result_student_information_college_name = result_student_information_college_name
		 	}
		});
	},
																															/**
	 * 获取mentor_name
	 */
	get_mentor_information_mentor_name(){
		let url = "~/api/mentor_information/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "mentor_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_mentor_information_mentor_name = json.result.list;
			result_mentor_information_mentor_name.map(o => o.title = o['mentor_name'])
	  			this.result_mentor_information_mentor_name = result_mentor_information_mentor_name
		 	}
		});
	},
						/**
	 * 获取title_of_supervisor
	 */
	get_mentor_information_title_of_supervisor(){
		let url = "~/api/mentor_information/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "title_of_supervisor": this.query.word }, (json) => {
		  if (json.result) {
			var result_mentor_information_title_of_supervisor = json.result.list;
			result_mentor_information_title_of_supervisor.map(o => o.title = o['title_of_supervisor'])
	  			this.result_mentor_information_title_of_supervisor = result_mentor_information_title_of_supervisor
		 	}
		});
	},
						/**
	 * 获取research_direction
	 */
	get_mentor_information_research_direction(){
		let url = "~/api/mentor_information/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "research_direction": this.query.word }, (json) => {
		  if (json.result) {
			var result_mentor_information_research_direction = json.result.list;
			result_mentor_information_research_direction.map(o => o.title = o['research_direction'])
	  			this.result_mentor_information_research_direction = result_mentor_information_research_direction
		 	}
		});
	},
																												/**
	 * 获取student_name
	 */
	get_application_for_registration_student_name(){
		let url = "~/api/application_for_registration/get_list?like=0";
				url = url+"&examine_state=已通过";
				this.$get(url, { page: 1, size: 10, "student_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_application_for_registration_student_name = json.result.list;
			result_application_for_registration_student_name.map(o => o.title = o['student_name'])
	  			this.result_application_for_registration_student_name = result_application_for_registration_student_name
		 	}
		});
	},
																		
  },
  components: { list_result_search },
	created(){
    this.query.word = this.$route.query.word || "";
  },
  mounted() {
	this.get_article();
					this.get_student_users_student_account();
										this.get_student_users_college_name();
							this.get_student_users_class_name();
								this.get_mentor_user_tutor_account();
																	this.get_student_information_student_name();
							this.get_student_information_student_no();
													this.get_student_information_college_name();
																																this.get_mentor_information_mentor_name();
							this.get_mentor_information_title_of_supervisor();
							this.get_mentor_information_research_direction();
																													this.get_application_for_registration_student_name();
																		  },
  watch: {
	$route() {
	  $.push(this.query, this.$route.query);
	  this.get_article();
				  this.get_student_users_student_account();
									  this.get_student_users_college_name();
						  this.get_student_users_class_name();
							  this.get_mentor_user_tutor_account();
																  this.get_student_information_student_name();
						  this.get_student_information_student_no();
												  this.get_student_information_college_name();
																															  this.get_mentor_information_mentor_name();
						  this.get_mentor_information_title_of_supervisor();
						  this.get_mentor_information_research_direction();
																												  this.get_application_for_registration_student_name();
																			},
  },
};
</script>

<style scoped>
.card_search {
  text-align: center;
}
.card_result_search>.title {
  text-align: center;
  padding: 10px 0;
}
</style>
