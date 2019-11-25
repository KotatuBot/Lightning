<template>
  <div class="sourceview">
                        <h3> SoureTEST</h3>
			<tr v-for="code in codeview" v-bind:key="code.id">
				<td v-on:click="onwrite(code.id)">{{code.id}}</td>
				<td class="codeline">{{ code.content }}</td>
                                <div v-if="code.mflag">
                                        <button v-on:click="display_memo(code.id)">+</button>
                                </div>
			</tr>
		<hr/>
		<button v-on:click="data_send">Send</button>


                <div v-if="flag" class="codeline">
			<div>
				<textarea name="comment" cols="30" rows="5" v-model="message"></textarea>	
                                <button v-on:click="adding_memo(currentnumber)" class="btn btn-secondary">Send</button>
			</div>
                
                </div>

                <div>
                        <div v-for="code in codeview" v-bind:key="code.id">

                                <div v-if="code.dflag">
                                        <div class="codeline">
                                                <h3>{{code.id}} line</h3>
                                                <hr>
                                                <p>{{code.message}}</p>
                                        </div>

                                </div>


                        </div>
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
                message: '',
                writeing_memo: [],
                flag: false,
                
          }
  },

 methods: {

	data_send: function(event){
	if(event){

		var code_data = "<?php\n\ngila::controller('blog', 'blog/controllers/blog', 'Blog');\n";
		var code_list = code_data.split('\n');

		for (var number=0;number<code_list.length;number++){

			var tmp = {id:number,content:code_list[number],flag:false,message:'',mflag:false,dflag:false}
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
        },

        adding_memo: function(index){

                for(var j=0;j<this.codeview.length;j++){
                        if(j===index){
                               this.codeview[j].mflag = true;
                               this.codeview[j].message = this.message;
                        }       
                        
                 }

                var tmp = {}
                tmp['id']=index
                tmp['memo']=this.message;
                this.writeing_memo.push(tmp)
                this.message = "";
                this.flag = false;
                
        },

        display_memo: function(index){
                for(var s=0;s<this.codeview.length;s++){
                        if(s===index){

                               if(this.codeview[s].dflag==false){
                                        this.codeview[s].dflag = true;
                               }else{
                                       
                                        this.codeview[s].dflag = false;        
                               }
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
