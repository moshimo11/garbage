/* eslint-disable */
<template>
	<div style="background-color: #FFFFFF;">
		<img id="logo" src="~@/assets/logo.jpg" alt="electron-vue">
        <div class="theme">针对当前疫情形势的城市智慧垃圾分类识别系统</div>
		
		
		<el-row style="padding: 22px;">
			<el-col :span="12">
				
				<el-card class="box-card"  :body-style="{ padding: '0px', height: '60%'}">
					<img src="http://127.0.0.1:5000/video_img_url" class="image" ></img>//视频流
				</el-card>
			</el-col>
			<el-col :span="8" :offset="2">
			<img src="static/bar2.png" class="image"></img>
				<el-col :offset="5">
					
			<el-button type="success" round @click ="takeAPhotho()"><i class="el-icon-camera"></i>拍照</el-button>
			</el-col>
			</el-col>
		</el-row>
		
		<el-steps :active="3" align-center style="padding: 40px;">
			<el-step title="步骤1" description="将待分类的垃圾放置于垃圾平台上,待屏幕可以正确显示位置"></el-step>
			<el-step title="步骤2" description="点击屏幕上的拍照按钮,等待机器进行垃圾识别分类"></el-step>
			<el-step title="步骤3" description="机器识别成功,等待打开相应的垃圾桶"></el-step>
		</el-steps>
		
		
		
		
	</div>

</template>

<script>
	var self;
	export default{
		data() {
			return{
				src: 'https//likecy.oss-cn-beijing.aliyuncs.com/0194a25dcd1b46a8012053c074fa37.jpg@2o_1574846777533.jpg'
			}
		},
		created: function(){
			self =this;
		},
		methods:{
			GoToResult(){
				this.$router.push('./result')
			},
			},
			takeAPhotho(){
				this.$http.get('http://192.168.137.241:5000/shut_photho',{    
				}).then(function(res){
					// alert(res.data);
					self.$message({
				// ShowClose: ture,
				message: res.data,
				type: 'success'
					});
					self.deltailDataFromServers(res.data);
					console.log(error);
				}).catch(function(error){
					console.log(error);
				});
			},
			deltailDataFromServers(data){
				var result=data.split("/");
				switch(result[0]){
					case "可回收物":
						self.$router.push({name:'result',params:{
							channel:0
						}});
						break;
					case "其他垃圾":
						self.$router.push({name:'result',params:{
							channel:1
						}});
						break;					
					case "厨余垃圾":
						self.$router.push({name:'result',params:{
							channel:2
						}});
						break;
					case "有害垃圾":
						self.$router.push({name:'result',params:{
							channe:3
						}});
						break;
					case "废弃口罩":
						self.$router.push({name:'result',params:{
							channel:4
						}});
						break;
				}

					

				}
			}
		}
</script>
	
<style>
	.image{
		width: 50%;
		height: 60%;
	}

</style>



  .theme {
    color: #2c3e50;
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 6px;
    justify-content:center;
  }

  .left-side {
    display: flex;
    flex-direction: column;
    justify-content:center;
  }