#Thinkphp常见问题1
***

###Thinkphp模板变量  
***
	__ROOT__：/root
	__APP__：/root/index.php
	__MODULE__：/root/index.php/Admin
	__CONTROLLER__：/root/index.php/Admin/Index
	__ACTION__：/root/index.php/Admin/Index/index
	__SELF__：/root/index.php/Admin/Index

###文件相对路径
>1.比如blog项目在/var/www/html/blog，还有/var/www/html/test，那么：  
>2.在项目中使用$url = "../test"的表示进入到test目录，因为thinkphp里面的文件的当前出口都是index.php

###Thinkphp中mysql相关的测试方案
>写错一个字段，打印出来，然后再navicat进行测试。  
>$Log->where($where)->filed(*.log,ttttt)->select();

###继承父类的构造方法**parent::_initialize();**
	namespace Admin\Controller;
	use Think\Controller;
	class SystemController extends CommonController {
		public $url;
		public function _initialize(){
	
			parent::_initialize();
	
			$this->url = "http://www.bestsilence.top";
		}
	}
	
	namespace Admin\Controller;
	use Think\Controller;
	class CommonController extends Controller{
		protected function _initialize(){
	        if (!$Rbac::AccessDecision()) {
	            //检查认证识别号
	            if (!$_SESSION [C('USER_AUTH_KEY')]) {
	            	echo '<script type="text/javascript">window.top.location="'.__MODULE__.'C("USER_AUTH_GATEWAY")";</script>';
	            }else{
	              	$this->jret(1,'该操作的权限受到了限制');
	                exit;
	            }
	        }
		}
	}