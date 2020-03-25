---
title: ofo小黄车数据库搭建
tags:
  - Good
  - ofo
url: 50.html
id: 50
categories:
  - Computer
date: 2018-04-13 22:37:46
---

想法源于一次对于Github的检索。 ofo小黄车的一大卖点便是其独特的密码解锁方式，但由于初期ofo自行车智能锁不具备更换密码的功能，故设计并建立此数据库。

原理：
===

网站首页添加查询密码和录入密码的功能。在查询的同时可以将未收录的密码通过录入的方式以扩大数据库。 录入数据库部分PHP代码：

     <meta charset="UTF-8">
    <script>alert("导入成功！！！")</script>
    <html>   
    <head>   
    <meta http-equiv="refresh" content="0.1;  
    url=<?php echo "http://www.wangyuyang.top/xhc/lu.php";?>">   
    </head>   
    <body>   
    页面只停留一秒……   
    </body> 
    </html>
    <?php
    /**
     * =======================================
     * Created by WeiBang Technology.
     * User: Wei ZhiHua
     * Date: 2016/10/12 0021
     * Time: 下午 4:14
     * Power: 实现验证码功能
     * =======================================
     */
        $url = "http://www.wangyuyang.top/xhc/lu.php"; 
    
    $pass =  strtolower($_REQUEST['password']);
    
    $num =  strtolower($_REQUEST['bikeNum']);
    echo $num ;
    if (isset($_REQUEST['authcode'])) {
        session_start();
        if (strtolower($_REQUEST['authcode']) == $_SESSION['authcode']) {
            echo ("Succeed ! ! ! ") ;
           $con = mysql_connect("*******.my3w.com","*********","**********");
        if (!$con)
          {
          die('Could not connect: ' . mysql_error());
          }
    
        mysql_select_db("*******_db", $con);
    
        mysql_query("replace into xhc(bikeNum, password) values($num, $pass);");
    
        echo "Done!";
        header('Location: http://www.wangyuyang.top/xhc/lu.php');
        header('Refresh:3,Url=lu.php');
    
        mysql_close($con);
        }  
    
        else {
           echo ("Failed! ! !");
        }
        header('Location: http://www.wangyuyang.top/xhc/lu.php');
        exit();
    
    
    }
    ?>
    
    
    
    

首页部分代码：

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
        <link rel="stylesheet" href="./style.css">
        <title>ofo密码查询数据库</title>
    </head>
    <body>
    <div class="container">
        <div class="tips">
          <h3>请输入ofo车牌号，程序将自动查询密码数据库。</h3>
            <h3>若存在密码将在下方显示。</h3>
            <?php
            $link = mysql_connect("*******.my3w.com","*******","*******");
            mysql_select_db("*******_db", $link);
    
        $result = mysql_query("SELECT COUNT(*) FROM xhc", $link);
        list($num_rows) = mysql_fetch_row($result);
        echo "当前数据总数:$num_rows  条\n";
        ?>
            <h5>若还未收录，欢迎您的录入，您小小的举动将帮助无数的骑友</h5>
        </div>
            <div>
                <input type="text" name="bikeNum" placeholder="车牌号" id="bikeNum">
            </div>
            <div style="margin-top: 20px">
                <input type="text" style="height:55px;font-size:35px;color:#FF0000;" name="password" placeholder="密码将显示在这里" disabled="true"  id="password">
            </div>
            <div style="margin-top: 20px">
                <div class="btn-round" style="margin-top: 20px;background-color: #12c87d" onclick="fn_seach()">查询</a>
            </div>
        <a href="lu.php" class="btn-round" style="margin-top: 20px">录入</a>
    </div>
    <script>
        function fn_seach(){
                var xhr = new XMLHttpRequest();
                var bikeNum = document.querySelector('#bikeNum').value;
                xhr.onreadystatechange = function()
              {
              if (xhr.readyState==4 && xhr.status==200)
                {
                    document.getElementById("password").value=xhr.responseText;
                    alert("查询成功！！！\n 密码是："+ xhr.responseText +"\n" +"如果密码错误，请点击‘录入’对密码进行更正，感谢您的支持！")
    
                }
              }
                xhr.open("get","./search.php?bikeNum="+ bikeNum,true);
                xhr.send();
            }
        </script>
    </body>
    </html>
    
    
    

查询部分PHP代码:

    
    <?php
    $servername = "**********.my3w.com";
    $username = "**********";
    $password = "**********";
    $dbname = "**********_db";
    
    // 创建连接
    $conn = new mysqli($servername, $username, $password, $dbname);
    // 检测连接
    if ($conn->connect_error) {
        die("连接失败: " . $conn->connect_error);
    } 
    
    $sql = "SELECT password FROM xhc where bikeNum = '$_GET[bikeNum]' " ;
    $result = $conn->query($sql);
    
    if ($result->num_rows > 0) {
        // 输出每行数据
        #$a = $result->num
        while($row = $result->fetch_assoc()) {
            echo  $row["password"];
    
            #if ($a > 1 ){
    
           ## }
           # $a = $a - 1
        }
    } else {
        echo "OPS！未找到,欢迎您前去录入！";
    }
    $conn->close();
    ?>
    

网站：
===

网站部分比较简单，一个首页负责呈现网页信息，一个录入数据页面，同时外加一个写出数据至数据库的功能php，目前不能防止SQL注入。 \[caption id="attachment\_13595" align="alignnone" width="1280"\]\[caption id="attachment\_14538" align="alignnone" width="1280"\]![首页图片](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-98.jpg) 首页图片\[/caption\] 首页图片\[/caption\]