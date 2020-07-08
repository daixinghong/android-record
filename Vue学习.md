* <h3>引用Vue.js</h3>
	* 开发环境 
	* 生产环境
* <h3>hello Vue!</h3>
		<div id="xixi">
    		{{ datas }}
		</div>
		 var app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue!'
        }
   		})



* <h3>数据引用</h3>
	
		var data = {a: 1}
	
	    var vm = new Vue({
	        el: "#xixi",
	        data: {
	            datas: data
	        }
	    })
	
	    console.log("data  " + data.a)
	    console.log("vm   " + vm.datas.a)
	    if (vm.datas.a == data.a) {
	        console.log("数组相等")
	    }
	
* <h3>条件表达式</h3>
	* 关键字 v-if=''
	
				<div id="visable">
    			<p v-if = 'visable'>看得到我</p>
				</div>

				new Vue({
        		el:"#visable",
        		 data:{
           		 visable:false
       	 		}
   					 })

* <h3>循环</h3>

		<div id="for_item">
	
	    <ol>
	        <li v-for='item in list'>
	            <p>{{item.text}}</p>
	        </li>
	
	    </ol>
	
	</div>

		new Vue({
	        el: "#for_item",
	        data: {
	            list: [{"text": "哈哈"}, {"text": "嘻嘻"}, {"text": "呵呵"}]
	        }
	    })

* <h3>处理用户点击事件</h3>
	* 关键字 v-on:click='xx'  
	
			<div id="click">
				 <p>{{message}}</p>
				 <button v-on:click="showMessage">点击事件</button>
		
			</div>

				new Vue({
		        el: "#click",
		        data: {
		            message: "ha hah"
		        },
		        methods: {
		            showMessage: function () {
		                this.message = this.message.split(" ")[0]
		            }
		        }
		    })

* <h3>用户输入</h3>
	* 用于用户输入和显示的双向绑定关键字 v-model=''
				<div id="input">
		
				 <p>{{message}}</p>
					<input v-model='message'>
				</div>

				  new Vue({
				        el: '#input',
				        data: {
				            message: 'hello'
				        }
				    })

* <h3>组件化应用构建</h3>
	* 关键字 Vue.component（"组件名称",{templlate:'包装的内容'}）
	* 直接使用组件名称（tool-item）

			<div id="counts">
		   	   <ol>
		
		        <tool-item v-for='array in arrays' v-bind:array = 'array' v-bind:index =array.id >
		
		        </tool-item>
		
		    </ol>
		
		</div>
	
			 Vue.component('tool-item', {
			        props:['array','index'],
			        template: '<li>{{array.text}}+{{index}}</li>'
			    })
			
			    new Vue({
			        el: '#counts',
			        data: {
			            arrays: [{text:'菠萝',id:0}, {text:'橘子',id:1}, {text:'西瓜',id:2}]
			        }
			    })