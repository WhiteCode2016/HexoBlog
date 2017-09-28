---
title: SpringBoot Shiro登录验证处理
date: 2017-09-28 09:14:04
categories:
	- SpringBoot
	- Shiro
---
###### 这里我们将通过Filter来拦截抛出的登录异常，来处理登录过程中所出现的错误信息
###### 下面是我们所抛出的异常，见[Github](https://github.com/WhiteCode2016/WhiteCode/blob/master/whitecode-core/src/main/java/com/whitecode/shiro/SystemShiroRealm.java)
  ```java
	if (sysUser == null) {
        throw new UnknownAccountException();
    } else if (!password.equals(sysUser.getPassword())) {
        throw new IncorrectCredentialsException();
    } else if (sysUser.getStatus() == StatusEnum.LOCKED) {
        throw new LockedAccountException();
    } else if (sysUser.getStatus() == StatusEnum.DISABLED) {
        throw new DisabledAccountException();
    }
  ```
<!-- more -->
##### 1、登录失败处理
###### 登录失败的原因包括：UnknownAccountException(账号不存在)、IncorrectCredentialsException(密码不正确)、LockedAccountException(账号锁定)、DisabledAccountException(账号禁用)等，都是以JSON的格式返回错误信息
  ```java
	@Override
	protected boolean onLoginFailure(AuthenticationToken token, AuthenticationException e, ServletRequest request, ServletResponse response) {
		if (!ShiroFilterUtil.isAjax(request)) {
			setFailureAttribute(request, e);
			return Boolean.TRUE;
		}
		JsonResult jsonResult = new JsonResult();
		String message = e.getClass().getSimpleName();
		if ("IncorrectCredentialsException".equals(message)) {
			jsonResult = JsonResultUtil.error(ResultEnum.LOGIN_PASSWORD_ERROR);
		} else if ("UnknownAccountException".equals(message)) {
			jsonResult = JsonResultUtil.error(ResultEnum.LOGIN_ACCOUNT_ERROR);
		} else if ("LockedAccountException".equals(message)) {
			jsonResult = JsonResultUtil.error(ResultEnum.LOGIN_LOCK_ERROR);
		} else if ("DisabledAccountException".equals(message)) {
			jsonResult = JsonResultUtil.error(ResultEnum.LOGIN_DISABLED_ERROR);
		} else if ("CaptchaException".equals(message)) {
			jsonResult = JsonResultUtil.error(ResultEnum.CAPTCHA_ERROR);
		} else {
			jsonResult = JsonResultUtil.error(ResultEnum.UNKONW_ERROR);
		}
		ShiroFilterUtil.out(response,jsonResult);
		return Boolean.FALSE;
	}
  ```
#### 2、登录成功处理
  ```java
	@Override
	protected boolean onLoginSuccess(AuthenticationToken token, Subject subject, ServletRequest request, ServletResponse response) throws Exception {
		if (!ShiroFilterUtil.isAjax(request)) {
		   issueSuccessRedirect(request, response);
			return Boolean.TRUE;
		}
		ShiroFilterUtil.out(response,JsonResultUtil.success(ResultEnum.LOGIN_SUCCESS));
		return Boolean.FALSE;
	}
  ```
#### 3、登录处理
  ```java
	@Override
	protected boolean executeLogin(ServletRequest request, ServletResponse response) throws Exception {
	    if (!ShiroFilterUtil.isAjax(request)) {
	        return Boolean.TRUE;
	    }
	    CustomUsernamePassordToken token = createToken(request,response);
	    try {
	        // 校验验证码（去掉，可不使用验证码）
	        // doCaptchaValidate((HttpServletRequest) request,token);
	        Subject subject = getSubject(request, response);
	        subject.login(token);
	        return onLoginSuccess(token, subject, request, response);
	    } catch (AuthenticationException e) {
	        return onLoginFailure(token,e,request,response);
	    }
	}
  ```	
###### 详细代码见 [Github](https://github.com/WhiteCode2016/WhiteCode/blob/master/whitecode-core/src/main/java/com/whitecode/shiro/filter/LoginFilter.java)