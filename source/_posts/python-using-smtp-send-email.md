title: python使用smtp发送邮件
tags:
  - AUTH
  - python
  - smtp
  - tls
id: 605
categories:
  - Python
date: 2013-11-02 14:28:58
---

python中使用smtp发送邮件十分简单

	import smtplib   
	
	smtp = smtplib.SMTP()   
	smtp.connect("smtp.domain.com", "25")   
	smtp.login('username', 'passowrd')   
	smtp.sendmail('from@domain.com', 'to@to.com', 'Testing Content.')   
	smtp.quit()
	
有一些邮箱服务器会需要TLS支持，如果不开其则会报错：

	raise SMTPException: SMTP AUTH extension not supported by server.

则connect后需要开启TLS，代码如下

	import smtplib   
	
	smtp = smtplib.SMTP()   
	smtp.connect("smtp.domain.com", "25")
	smtp.ehlo()
	smtp.starttls()
	smtp.login('username', 'passowrd')   
	smtp.sendmail('from@domain.com', 'to@to.com', 'Testing Content.')  
	smtp.quit()