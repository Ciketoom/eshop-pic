<template>
	<div class="main">
	    <div class="header">
            <div class="logo"><img src="http://pic8.nipic.com/20100808/482358_183144041922_2.jpg" alt="logo"></div>
            <div class="nav">
                <h1>网站首页</h1>
                <ul>
                    <li>品牌介绍</li>
                    <li>新兴资讯</li>
                    <li>产品与技术</li>
                    <li>服务专区</li>
                    <li>学习专区</li>
                    <li>品牌加盟</li>
                    <li>联系我们</li>
                </ul>
            </div>
        </div>
        <div class="image">
            <img src="http://c.hiphotos.baidu.com/zhidao/pic/item/d000baa1cd11728bcdde8185ccfcc3cec2fd2ca1.jpg" alt="g">
        </div>
        <div class="font">
            <div class="tab">
                <h5>加盟入口</h5>
                <h5>加盟入口</h5>
            </div>
            <div class="font-main">
                <form class="contact_form" action="#" method="post" name="contact_form">
                    <ul>
                        <li class="usually"> 
                            <label><span class="xing">*</span>姓名:</label>
                            <input type="text" placeholder="请输入姓名" v-model="name" required />
                        </li>
                        <li class="usually">
                            <label><span class="xing">*</span>出生日期:</label>
                            <input type="date" placeholder="请选择日期" v-model="date" required />
                        </li>
                        <li class="usually">
                            <label><span class="xing">*</span>性别:</label>
                            <input class="red" type="radio" id="male" value="男" v-model="sex"> 男
                            <input class="red" type="radio" id="female" value="女" v-model="sex"> 女
                        </li>
                        <li class="usually">
                            <label><span class="xing">*</span>手机:</label>
                            <input type="tel" pattern="^1(3|4|5|6|7|8|9)\d{9}$" placeholder="请输入手机号码" v-model="phone" required />
                        </li>
                        
                        <li class="usually">
                            <label>注册邮箱:</label>
                            <input type="email" placeholder="12345678@qq.com"  v-model="email" required />
                        </li>
                        <li class="usually">
                            <label>微信号:</label>
                            <input type="text" placeholder="请输入微信号" v-model="wechat" required />
                        </li>
                        
                        <li class="usually">
                            <label><span class="xing">*</span>实体店经验:</label>
                            <input type="radio" id="have" value="有" v-model="jing"> 有
                            <input type="radio" id="shi" value="无" v-model="jing"> 无
                            
                        </li>
                        <li class="usually">
                            <label><span class="xing">*</span>计划开店面积:</label>
                            <input type="radio" v-model="mian" value="20~80平方米" id="small"/>20~80平方米
                            <input type="radio" v-model="mian" value="80平方米以上"  id="big"/>80平方米以上
                        </li>
                        <li class="usually">
                            <label><span class="xing">*</span>意向区域:</label>
                            <v-distpicker 
                                class="xuan"
                                :province="province" 
                                :city="city" 
                                :area="area"
                                @selected="onSelected">
                            </v-distpicker>
                        </li>
                        <li class="usually">
                            <label><span class="xing">*</span>详细地址:</label>
                            <input placeholder="请输入详细地址" type="text" v-model="address" required />
                        </li>
                        <li v-if="address!=''">
                            <baidu-map 
                            :center="center" 
                            :zoom="zoom" 
                            @ready="handler" 
                            :scroll-wheel-zoom='true'
                            style="height:250px;width:550px" 
                            @click="getClickInfo">
                                <bm-map-type :map-types="['BMAP_NORMAL_MAP', 'BMAP_HYBRID_MAP']" anchor="BMAP_ANCHOR_TOP_LEFT"></bm-map-type>
                                <bm-geolocation anchor="BMAP_ANCHOR_BOTTOM_RIGHT" :showAddressBar="true" :autoLocation="true"></bm-geolocation>
                                <bm-navigation anchor="BMAP_ANCHOR_TOP_RIGHT"></bm-navigation>
                                <bm-marker :position="center" :dragging="true"  @click="infoWindowOpen">
                                    <bm-info-window style="width:200px" :show="show" @close="infoWindowClose" @open="infoWindowOpen"><p>{{dianadd}}</p></bm-info-window>
                                </bm-marker>
                                <bm-local-search :keyword="add" :auto-viewport="true" :location="location" zoom="20" style="display: none"></bm-local-search>
                            </baidu-map>
                        </li>
                        <li class="usually">
                            <label>其它意向地址1:</label>
                            <input placeholder="请输入意向地址1" type="text" v-model="address1" required />
                        </li>
                        
                        <li class="usually">
                            <label>其它意向地址2:</label>
                            <input placeholder="请输入意向地址2" type="text" v-model="address2" required />
                        </li>
                        <li >
                            <a @click="tijiao()">提交</a>
                        </li>
                    </ul>
                </form>
            </div>
        </div>
        <div class="footer">
			<div class="footer_up">
				<div class="footer_l">
					<h5>品牌介绍</h5>
					<ul>
						<li>特色介绍</li>
						<li>热门商品</li>
						<li>常见问题</li>
						<li>联系客服</li>
					</ul>
				</div>
				<div class="footer_c">
					<h5>新闻资讯</h5>
					<ul>
						<li>配送服务</li>
						<li>24小时服务</li>
						<li>联系客服</li>
					</ul>
				</div>
				<div class="footer_r">
					<h5>产品和技术</h5>
					<ul>
						<li>配送服务</li>
						<li>24小时服务</li>
						<li>联系客服</li>
					</ul>
				</div>
				<div class="footer_rr">
					<h5>学习专区</h5>
					<ul>
						<li>配送服务</li>
						<li>特色专业定制</li>
						<li>大众喜爱</li>
					</ul>
				</div>
                <div class="footer_rrr">
					<h5>咨询热线</h5>
					<h1>020-5426-999</h1>
                    <p>乐意为您服务</p>
				</div>
			</div>
            <div class="footer_down">	   
                <h1><span>版权所有   广东某某有限公司</span>地址：广东省东莞市南城区某某街道</h1>
                <h1>本网站由广东某某有限公司技术支持    编号1564845341</h1>
            </div>
		</div>
    </div>
</template>

<script>	
	import axios from 'axios'
	export default {
		data() {
			return{
                name:'',
                date:'',
                phone:'',
                email:'',
                wechat:'',
                sex:'',
                mian:'',
                jing:'',
                province:'',
                city: '',
                area: '',
                address:'',
                address1:'',
                address2:'',
                baddress:'',
                dianadd:'',
                location: '',
                center: {lng: 109.45744048529967, lat: 36.49771311230842},
                zoom: 22,
                show: false, //窗口提示开关
                BMap: null, // 地图组件是否就绪
			}
		},	
		computed:{
            add:function(){
                if(this.address!=''){
                    return this.province+this.city+this.area+this.address
                }    
            },
        },		
		methods:{			
			tijiao() {	   
                let params ={
                    name:this.name,
                    sex:this.sex,
                    phone:this.phone,
                    email:this.email,
                    wechat:this.wechat,
                    date:this.date,
                    mian:this.mian,
                    jing:this.jing,
                    address:this.add,
                    address1:this.address1,
                    address2:this.address2
                }   
                console.log(params) 
                let result = !Object.values(params).some(v=>v==''); 
                console.log(result) 
                if(result==true){
                    console.log(3) 
                    alert('提交成功')
                    axios.post("/users/test",{
                        params:params
                    }).then((response)=>{
                        let res = response.data;
                        if(res.status=="0") {
                            this.errorTip1 = false;
                            alert('成功')
                        }else{	
                           alert('失败')
                        }
                    })
                }      	
    			
            },
            handler ({BMap, map}) {
                this.BMap = BMap; //获取地图实例
            },
            //点击地图获取地址

            getClickInfo (e) {
                console.log(e.point.lng)
                console.log(e.point.lat)
                this.center.lng = e.point.lng
                this.center.lat = e.point.lat 
                console.log(this.center) 
                
                let myGeo =new this.BMap.Geocoder({extensions_town: true});      
                // 根据坐标得到地址描述    
                myGeo.getLocation(e.point,rs=>{  
                    console.log(rs)          
                    this.dianadd =rs.address 
                    this.province =rs.addressComponents.province
                    this.city =rs.addressComponents.city
                    this.area =rs.addressComponents.district
                    var a =rs.addressComponents.street
                    var b =rs.addressComponents.streetNumber
                    if(b!=''){
                        this.address =a+b
                    }else if(a==''){
                        this.address =' '
                    }   

                });
            },
            infoWindowClose () {
                this.show = false
            },
            infoWindowOpen () {
                this.show = true
            },
            //选择省市区
			onSelected(data) {
                this.province=data.province.value
                this.city=data.city.value  
                this.area=data.area.value
                console.log(this.province,this.city,this.area)
            },
		}
	}
</script>

<style lang="scss">
.main{
    position: relative;
    width:1903px;//可拿视口宽度
    margin: 0 auto;
    background: rgb(248, 228, 201);
    padding-top: 60px;
    .header{
        position: fixed;
        left: 0;
        top: 0;
        z-index: 10;
        width:100%;
        height: 60px;
        line-height: 60px;
        display: flex;
        justify-content: space-around;
        flex-direction: row;
        width:100%;
        background: rgb(246, 210, 162);
        .logo{
            width: 80px;
            height: 45px;
            margin-top: 10px;
            margin-left: 100px;
            img{
                width: 100%;
                height: 100%;
            }
        }
        .nav{
            font-size: 14px;
            width: 900px;  
            h1{display: inline-block;}
            ul{
                display: inline-block;
                li{
                    display: inline-block;
                    position:relative;
                    
                    padding: 0 5px;
                }
                li:nth-child(6){
                    color:red;
                   &::after{border-color: red transparent transparent transparent;}
                }
                li:after{
                    content: '';
                    position: relative;
                    top:10px;
                    width:0;
                    height:0;
                    border-width: 5px;
                    border-style: solid;
                    border-color: rgb(29, 29, 28) transparent transparent transparent;
                }
            }
        }
    }
    .image{ 
        width: 100%;
        height: 300px;
        img{
            width: 100%;
            height: 100%;
        }
    }
    .font{ 
        text-align: center; 
        font:14px bold "Microsoft Yahei";
        .tab{
            h5{display: inline-block;font-size: 14px;padding: 10px 5px;}
            h5:nth-child(2){color:rgb(219, 45, 45)}
        }
        .font-main{
            padding: 40px 0;
            text-align: left; 
            .contact_form{
                position: relative;
                left: 50%;
                transform: translateX(-50%);
                background:#fff;
                padding: 20px 50px;
                width:55%;
                ul{
                    width: 700px;
                    margin: 0 auto;
                    li{
                        padding: 10px 10px 10px 70px;  
                        .xing{color: red;}
                        label{
                            width:150px;float: left; text-align:right;
                        }  
                        
                        input{
                            margin-left: 10px;
                            border: 1px solid #999;
                            padding: 1px 5px;
                            text-align: left;
                        } 
                        .red{
                            background-color: red;
                        }
                        .xuan{
                            display:inline-block;
                            padding: 5px;
                            margin-left: 20px;
                            select{
                                height: 25px;
                                font-size: 14px;
                                padding: 0;
                            }
                        }  
                    }
                    li:last-child{
                        text-align: center;padding: 10px;
                        a{
                            background: red;color: #fff;
                            padding:8px 10px;
                            font-size: 14px;
                        }
                     }
                }
                
            }
            

        }
    }
    .footer{
		width: 100%;
        
		.footer_up{
			height: 200px;
            padding: 10px 20%;
            background: rgb(230, 54, 54);	
            color: #fff;	
			h5{
				font-size: 16px;
				height: 50px;
				line-height: 50px;
				font-weight: 800;	
			}
			li{
				height: 20px;
				line-height: 20px;
				font-size: 12px;
				padding:7px 0;
				&:hover{
					cursor: pointer;
					color: #000;
				}
			}
			.footer_l{
				float: left;
				width:150px;		
			}
			.footer_c{
				width:150px;
				float: left;			
			}
			.footer_r{
				width:150px;
				float: left;	
			}
            .footer_rr{
				width:150px;
				float: left;	
			}
			.footer_rrr{
				width:150px;
				float: left;
                margin-left: 100px;
                h1{font-size: 24px;}
                p{padding: 20px 0;}	
			}
		}
        .footer_down{
            height: 60px;
            padding: 10px 20%;
            background: rgb(179, 36, 36);
            font-size: 14px;
            text-align: center;
            color:#fff;
            h1{
                height: 25px;
                line-height: 25px;
                span{margin-right: 40px;}
            }	
        }		
	}
}
</style>