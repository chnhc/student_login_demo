# student_login_demo
Spring boot 初学 -- 学生登录demo


// 先试 springboot - controller - dao

// springboot 请求过程  -- 看视频 spring boot 

// 请求处理- 拦截 。。。 SpringMVC 的配置

// 切面 @Aspect  切点 @Pointcut   切面前@Before   切面后@After  --  环绕 @Around

// 自定义注解 ，实现  切面 + 自定义注解 处理controller前的事情  

// 统一异常 、 统一返回



   


1 、建立 学生库


	-- 学生表
	    id 主键 自增		1
	    stu_phone   手机号	18316610102
	    stu_name    名字		李静
	    stu_identity 身份证	123456
	    login_status 登录状态	 0 未登录 ，1 已登录，默认0
	
	-- 验证码表
	    id 主键 自增
	    stu_phone    	手机号
	    yzm     	验证码
	    yzm_status	验证码状态 0 未使用 ，1 已经使用，默认0
	    create_time	验证码创建时间
	    



业务 -- 学生登录操作
	--账号： 手机号
	--密码： 身份证
	--验证码：动态



通过手机号获取验证码，然后用验证码登录

	
	
	
业务流程：

 	获取验证码：
	-- 校验手机号(11位，号段) - 生成4位验证码 - 存入数据库

	登录：
	-- 验证验证码：校验手机号(11位，号段) - 查数据库 (通过手机号获取验证码) - 验证码时效性(20s) 、验证码是否可用和匹配验证码- 更新验证码状态到1 （出现失败 ：统一返回） -- MVC拦截实现

	-- 验证手机号身份证login()：查询数据库- 验证手机号身份证(不匹配：统一异常) - 返回实体：phone=手机号码、name=名字（ 统一返回）

	-- 切面 + 自定义注解 - 动态指定 login()，yzmLogin() 等   loginAspect() :  
	在login()前：
		控制台输出 手机号-验证码
	在login()执行完后：
		返回（ 统一返回）
		判断状code=200：
			phone=手机号码
			查询数据库 ：判断login_status 不等于1 ，可登录的 ，通过手机号码更新login_status = 1
				    判断login_status 等于1，已经有人登录， 返回 code= 201- 已经有人登录
			
		
	

	





