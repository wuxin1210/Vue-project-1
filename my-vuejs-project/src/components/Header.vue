<template>
	<div id="main"> 
	<header>
			<div class="loadingDiv" v-if="loading"></div>
			<div class="bd">
				<router-link to="/index">
				</router-link>
			</div>
			<span class="ipt">
				<i class="iconfont icon-fangdajing"></i>
				<input type="text"  placeholder="请输入关键词"/>
			</span>
		<div class="kefu">
	   <router-link to="">
	   	在线客服
	   </router-link>
		</div>
	</header>
	<commom-carousel></commom-carousel>
	<common-footer></common-footer>
	</div>
</template>

<script>
	import { Indicator } from 'mint-ui'; // 加载中
	import axios from 'axios';
	import Carousel from '@/components/Carousel'
    import Footer from '@/components/Footer'
export default {
  name: 'common-header',
  data () {
    return {
       loading: false,
       arr_films: [],
       active:true
    }  
  },
  components: {
  	'commom-carousel' : Carousel,
      'common-footer' : Footer
  },
  beforeMount(){
  		Indicator.open({
			  text: '',
			  spinnerType: 'triple-bounce'
			});
  },
  mounted(){  	
  	$("#foot li:nth-of-type(1) a").css("color","#ca0e25")
  	this.getData();
  },
  	methods: {
	  getData() {
	  
				// 用逻辑判断防止用户点击多次。
				if(this.loading) {
					return;
				}				
				this.loading = true;
//				http://www.dinghuapai.cn/api/home/index
					axios.get('/api/home/index')
				.then((res)=>{
//					console.log(res);
//					this.arr_films = this.arr_films.concat(res.data.model.list);
					this.loading = false;
					 Indicator.close();
				     })
				.catch(function (error) {
						//console.log(error);
					});
			}
		}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

header {
    background: #ca0e25;width: 100%;max-width: 100%;height: 50px;box-shadow: 0 1px 3px rgba(0,0,0,.3);overflow: hidden;
    display: flex;justify-content: space-around;align-items: center;
      .bd {
		    height: 100%;width: 90px;margin-right: 20px;background:  url(http://www.dinghuapai.cn/wap/img/logo.png) no-repeat left center;background-size: 100% auto; 			 
		    a{
		    	display: flex;
		    } 	     			    
		 }
		 .ipt{
		     	  height:30px;display: flex;align-items: center;
		     	  border-radius:20px;background:#d85565;
		     	  padding-left:5px;
			     	  i{
			     	display:flex;color:#fff;
			      }
			      input{		      	border:0;background:transparent;color:#fff;padding:0 10px;
			      }
		     }
		  .kefu{
		  	a{
		  		color:#fff;font-size: 12px;
		  	}
		  }    
}
#main{
	width:100%;height:100%;display: flex;flex-direction: column;
}

</style>
