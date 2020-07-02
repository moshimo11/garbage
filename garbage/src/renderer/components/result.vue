<template>
	
	
	<el-container>
		<el-header style="padding: 40px;"><div class="text-olive texe-xxl">垃圾识别结果</div></el-header>
		<el-main style="background-color: #FFFFFF;">
			
			
			<el-row>
				<el-col :span="4" :offset="2" v-for="(item,index) in ClassList" :Key="index">
					<div :class="index==channel?'divcss5':''">
						<!--      <div class="divcss5">-->
						<el-card :body-style="{ padding: '0px'}">
							<img :src="item.url" class="image">
						</el-card>
					</div>

				</el-col>
				
			</el-row>
			
		
			<el-row style="padding-top: 3.125rem;">
				<el-alert
					title="带辅助性文字介绍"
					type="success"
					description="这是一句绕口令:黑化肥会........."
					:closable="false">
				</el-alert>
			</el-row>
			
			
			<el-row style="padding: 70px;">
				<el-col :span="18" :offset="7">
					<el-button type="danger" round @click="OpenMotor()">再次打开垃圾桶</el-button>
					<el-button type="success" round @click="GoToPredict()">再次识别</el-button>
				</el-col>
			</el-row>
			
			
			
			
		</el-main>
	</el-container>
	
	
	
	
</template>

<script>
	var self;
	export default{
		data(){
			return{
				src:'https://cube.elemecdn.com/6/94/4d3ea53c084bad6931a56d5158a48jpeg.jpeg',
				channel:'',
				ClassList:[{
					url:"static/image/1.png",
				},{
					url:"static/image/2.png",
				},{
					url:"static/image/3.png",
				},{
					url:"static/image/4.png",
				}]
			}
		},
		created:function(){
			console.log('creating 创建完毕状态**************************》');
			this.channel =this.$route.params.channel;
			this.OpenMotor();
			self =this;
		},
		methods:{
			GoToPredict(){
				this.$router.push('./predict')
			},
			},
			OpenMotor(){
				var channel = this.channel
				console.log("开始舵机")
				this.$notify({
					title: '垃圾桶通知',
					message: '垃圾桶即将打开',
					type: 'success'
				});
				this.$http.get('http//127.0.0.1:5000/open_motor?channel='+channel,{
				}).then(function(res){
					// alert(res.data);
					self.$notify({
						title:'垃圾桶通知',
						message:'垃圾桶已关闭',
						
					});
					console.log(res)
				}).catch(function(error){
					console.log(error);
				});
				
			}
		}
	}
	
	
	
</script>

<style>
	.image{
		width: 100%;
		display: block;
	}
	.divcss5{ border:solid 10px #e54d42;
	}
</style>
