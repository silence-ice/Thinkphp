#Thinkphp验证码生成  
***

	<?php
	/**
	 * 验证码生成
	 */
	public function verify_c(){  
		session_start();
	    $Verify = new \Think\Verify();  
	    $Verify->fontSize = 20;
	    $Verify->useCurve = false;
	    $Verify->length   = 4; 
	    $Verify->useNoise = false;
	    $Verify->fontttf = '4.ttf';
	    $Verify->imageW = 0;  
	    $Verify->imageH = 0;  
	    $Verify->entry();
	    session_write_close();
	}  
	
	<div class="left_f1 text15">验证码：</div>
	<div class="left pad888 pad999">
	  <input name="verifyCode" type="text" class="input2" style="padding: 14px;" id="verifyCode" value=""/>
	</div>
	 <div class="left pad999">
	 	<img id="code" class="code" src="__APP__/Home/Public/verify_c" onclick="reflshCode()" />
	 </div>
	 <div class="left text14"><a class="reflesh" href="javascript:;" onclick="reflshCode()" title="看不清，换一张"><img src="__PUBLIC__/img/refrash.png" alt="看不清，换一张" /></a></div>
	 <div class="clear">
	</div>
	
	//点击更换图片
	reflshCode : function(){
	    $("#verify").val('');
	    var verifyCode = $("#code");
	    var t = new Date().getTime();
	    verifyCode.attr("src", app+"/Home/Public/verify_c?t="+t);
	}
	
	// 检测输入的验证码是否正确，$code为用户输入的验证码字符串
	function check_verify($code, $id = ''){    
		 $verify = new \Think\Verify(); 
		return $verify->check($code, $id);
	}