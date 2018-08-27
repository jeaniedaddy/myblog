---
title: Mobile Status Guide
date: 2018-08-27 11:37:32
categories: [work]
tags: [work,Mobile Status]
---

## 원리
1.	PDA의 네트워크 연결시 PDA는 DHCP에 hostName을 전달
1.	DHCP는 해당 PDA에  Dynamic IP address 부여.
1.	네트워크 접속 성공후 PDA가 veles2pda에 접속시 IP 정보만 전달.
1.	Veles2pda은 이런  IP를 가진 Device가 접속되었다고 aJax를 통해 asset web app의 REST API를 POST Call 한다.
1.	Asset web app은 이 veles2pda에서 전달한 IP 정보로 hostName을 네트워크에 문의하여 찾아오고 가지고 있는 HostName리스트를 참조하여 로그를 기록한다.
1.	DHCP lease 기간동안은 dl Dynamic IP 와 hostName이 Key vs Value처럼 look up이 가능하다.

## 추가 업데이트 계획
*	각Location별로 변경이 필요한 부분은 고쳐서 쓰세요              
*	관련 파일 : (\\HKE.LOCAL\GLOVIS)  ->  ~\IT\ZZ00.SteveNo
*	현재 배포판으로 Required기능구현 완료.
*	Security(Login) 및 Graphical Presentation 2개 정도 추가 배포 할 수 있슴.

## 설치 가이드

1.	Project name : asset
1.	Project description
  1.	Java(1.8) Spring Boot Project
  1.	Mongo DB – Spring Data
  1. 	Gradle package manager
  1. 	Thymeleaf template engine
  1. 	Swagger REST API Doc
1.	How to install (DB and WEB on same server)
  1.	Install mongo DB
  1.	Create c:\DATA\DT folder for the DB location
  1.	Run mongo db
  ``` bash
    $ mkdir c:\DATA\db
    $ cd "c:\Program Files\MongoDB\Server\4.0\bin"
    $ mongod
  ```
  1.	Clone the project using Git
  ``` bash
    $ git clone https://github.com/jeaniedaddy/asset.git
  ```
  1.	Use Eclipse, IntelliJ or other IDE as you like
  1.	How to Run (under “asset folder”)
  ``` bash
  $  gradlew bootRun
  ```
  1.	How to compile (under “asset folder”)
  ``` bash
  $  gradlew build
  ```
  1.	Compiled jar will be located ~/asset/build/libs/XXX.jar
  1.	How to Run this Jar file on the production server
  ``` bash
  $  java –jar  XXX.jar
  ```
1.	Web App is set to use 8090 port : http://localhost:8090
1.	Web App has 1 REST API for logging
  1.	Under about tab you can access Swagger-UI page for REST API Doc and test.
1.	How to consume REST API from other application
  1.	EX. VELES2PDA (~/veles2pda/menu/top.asp)
    1.	Add jquery framework to VELES2PDA (file will be provided)
    ```js
    <script type="text/javascript" src="/VELES2PDA/libs/jquery-1.5.min.js"></script>
    ```
    1.	For cross servers add configuration for jQuery
    ```js
    <script language="javascript">
  		jQuery.support.cors = true;
    ```

    1.	Using jQuery.ajax, consume REST API of this project
    ```js
      $(document).ready(function(){
  		    var ip_address = '<%=Request.servervariables("REMOTE_ADDR")%>';
  		    var usr_id = '<%=sUserID%>';
  			var a_url="http://10.10.0.10:8090/mobilelog/save?ipAddress="+ip_address+ "&loginId=" + usr_id;
  			var s_data = "";
  		    $.ajax({
  			   type: 'POST',
  			   url: a_url,
  			   data: "{}",
  			   dataType: 'text',
  			   success: function( data ) {
  			   		//console.log("success");
  			   		//alert("success1");
  			   },
  			   error: function(xhr, status, error) {
  			      //console.log(error);
  			      //alert(error);
  			   }
  			});
  		});
  	</script>
    ```
## How to set PDA.
1.	Go to control panel, change computer name as you want
1.	Do cold reset and connect local network and check if hostname of the PDA is showing in DHCP, WiFi Controller ….
