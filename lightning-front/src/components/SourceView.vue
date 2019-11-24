<template>
  <div class="sourceview">
                        <h3> SoureTEST</h3>
			<tr v-for="code in codeview" v-bind:key="code.id">
				<td v-on:click="onwrite(code.id)">{{code.id}}</td>
				<td class="codeline">{{ code.content }}</td>
			</tr>
		<hr/>
		<button v-on:click="data_send">Send</button>


                <div v-if="flag" class="codeline">
			<form action="#" method="post">
				<textarea name="comment" cols="30" rows="5"></textarea>	
				<p>{{currentnumber}}</p>
			</form>
                
                </div>


  </div>
</template>

<script>
export default {
  name: 'SourceView',
  data: function(){
          return{
		codeview: [],
                currentnumber: 0,
                flag: false,
          }
  },

 methods: {

	data_send: function(event){
	if(event){

		var code_data = "<?php\n\ngila::controller('blog', 'blog/controllers/blog', 'Blog');\n";
		var code_list = code_data.split('\n');

		for (var number=0;number<code_list.length;number++){

			var tmp = {id:number,content:code_list[number],flag:false,message:''}
			this.codeview.push(tmp)
		}

	}

	},

        onwrite: function(code){
                for (var number=0;number<this.codeview.length;number++){

                        if (code===this.codeview[number].id){

                               this.flag = true;
				this.currentnumber = code;
                                
                             }
		}
        }
	

 },

}
</script>
<style>
.codeline{

	text-align: left;
	padding-left: 5%;
        padding-bottom: -100px;
	width: 500px;
        height: 3%;

}
</style>
