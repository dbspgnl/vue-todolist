<template>
  <div class="hello">
	<p class="my-header-blue">ToDo 리스트</p>
	<div class="content">
		<p><b>현재목록 : </b>{{todos.length}}건 중 {{remaining}}건 처리, {{overdate}} 완료일 지남</p>
		<input type="text" v-model.trim="addtext" v-on:keyup.enter="addToDo" placeholder="할일">
		/
		<input type="text" v-model.trim="dueDate" v-on:keyup.enter='addToDo' placeholder="완료일(YYYYMMDD)">
		<p>
			<button v-on:click="cleanToDo">처리완료삭제</button>
			<button v-on:click="sortData('todo')">이름순 정렬</button>
			<button v-on:click="sortData('data')">완료일 정렬</button>
		</p>
		<hr>
		<transition-group>
		<li v-for="(todo, index) in todos" v-bind:key="todo.DueDate" style="list-style-type:none;">
			<label>
				<input type="checkbox" v-model="todo.done">
				<span class="todoStyle" v-bind:class="{doneStyle:todo.done}">{{todo.text}}</span>
				<span v-bind:class="{doneStyle:todo.done}">&emsp;(완료일: {{todo.DueDate}})</span>&nbsp;
				<button class="small-button" v-on:click="extendDate(index)">완료일 연장</button>
			</label>
		</li>
		</transition-group>
	</div>

  </div>
</template>

<script>
export default {
	name: 'HelloWorld',
	data(){
		return {
			addtext:'',
			dueDate:'',
			todos:[
				{done:false, text:'계약서 작성', DueDate:"20200803"},
				{done:false, text:'프로젝트 기획', DueDate:"20200804"},
				{done:false, text:'어플리케이션 시연', DueDate:"20200817"},
				{done:false, text:'프로젝트 초안', DueDate:"20200805"},
				{done:false, text:'어플리케이션 개발', DueDate:"20200810"},
			]
		}

	},
	computed:{
		remaining: function(){ //완료된 개수
			return this.todos.filter(function(val){
				return val.done == true;
			}).length;
		},
		overdate: function(){ //기한을 넘긴 개수
			return this.todos.filter(function(val){
				var date = new Date(); //날짜 객체 생성
				var year = date.getFullYear();
				var month = new String(date.getMonth()+1); //0 부터 시작함
				var day = new String(date.getDate());
				//MM-DD형식
				if(month.length == 1) month = "0" + month;
				if(day.length == 1) day = "0" + day;
				var due_date = year+month+day;
				//필터 조건식
				return val.DueDate < due_date; //오늘 날짜보다 작은 Data의 날짜들
			}).length; //그 개수만큼 리턴
		}
	},
	methods:{
		addToDo: function(){ //리스트 추가 기능
			if(this.addtext){
				var due_date = this.dueDate; // data의 값을 새 변수에 넣음
				if(this.dueDate==''){ //만약 날짜를 입력하지 않았을 경우
					var date = new Date();
					date = new Date(Date.parse(date)+1*1000*60*60*24); //1일 뒤
					var year = date.getFullYear();
					var month = new String(date.getMonth()+1); 
					var day = new String(date.getDate());
					//MM-DD 형식
					if(month.length == 1) month = "0" + month;
					if(day.length == 1) day = "0" + day;
					due_date = year+month+day;
				}
				this.todos.push({done:false, text:this.addtext, DueDate:due_date});
				this.addtext='';
			}
		},
		cleanToDo: function(){ //완료 삭제 기능
			this.todos = this.todos.filter(function(val){
				return val.done == false;
			})
		},
		extendDate: function(index){ //기한 연장 기능
			var str_date = this.todos[index].DueDate; //해당 인덱스의 날짜값
			var y = str_date.substr(0,4); //연도
			var m = str_date.substr(4,2); //월
			var d = str_date.substr(6,2); //일
			//위 변수를 통해서 날짜 객체를 만든다.
			var date = new Date(Date.parse(new Date(y, m-1, d))+1*1000*60*60*24); //1일 후
			var year = date.getFullYear();
			var month = new String(date.getMonth()+1);
			var day = new String(date.getDate());
			if(month.length==1) month = "0" + month;
			if(day.length==1) day = "0" + day;
			var due_date = year+month+day;

			this.todos[index].DueDate = due_date; //data 값 교체
		},
		sortData: function(type){ //정렬 기능
			if(type=="todo"){
				this.todos.sort(function(a,b){ //글자 정렬
					console.log(a.text);
					console.log(b.text);
					console.log((a.text<b.text?-1:1));
					return (a.text<b.text? -1:1);
				});
			}else{
				this.todos.sort(function(a,b){ //날짜 정렬
					return (a.DueDate < b.DueDate ? -1 : 1)
				});
			}
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
