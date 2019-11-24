<template>
  <div class="sourceview">
                        <h3> SoureTEST</h3>
			<tr v-for="code in codeview" v-bind:key="code.id">
				<td>{{code.id}}</td>
				<td class="codeline">{{ code.content }}</td>
			</tr>
		<hr/>
		<button v-on:click="data_send">Send</button>


  </div>
</template>

<script>
export default {
  name: 'SourceView',
  data: function(){
          return{
		codeview: [],
          }
  },

 methods: {

	data_send: function(event){
	if(event){

		var code_data = "<?php\n\ngila::controller('blog', 'blog/controllers/blog', 'Blog');\n";
		var code_list = code_data.split('\n');

		for (var number=0;number<code_list.length;number++){

			var tmp = {id:number,content:code_list[number]}
			this.codeview.push(tmp)
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
	width: 1500px;

}
</style>
