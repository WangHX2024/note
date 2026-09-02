---
hide:
  - footer
  - feedback
title: 主页
---

<center><font  color= #518FC1 size=6>王浩雄的个人笔记</font>

<p><font color="#B9B9B9">记住我的名字，就不会忘记这个网站的地址 <b>https://note.haoxiong.wang</b></font></p>
</center>

<div class="grid cards" markdown>

-   :fontawesome-solid-code:{ .lg .middle } __提示__

    ---

    25-26春夏学期课程笔记《软件工程》《编译原理》已同步到本站~


</div>

<div class="grid cards" markdown>

-   :material-book-open-variant-outline:{ .lg .middle } __推荐阅读__

    ---


    - [x] [数字逻辑设计](/note/dld)

    - [x] [计算机体系结构](/note/ca)

    - [x] [数据库系统](/note/db)

    - [x] [面向对象程序设计](/note/oop)

    - [x] [离散数学](/note/dm)

    - [x] [软件工程](/note/se)

    - [x] [编译原理](/note/cp)



-   :fontawesome-solid-user-tag:{ .lg .middle } __关于我__

    ---


    - 王浩雄同学是浙江大学竺可桢学院混合班2023级本科生，主修专业为**计算机科学与技术**。

        [:octicons-arrow-right-24: 我的个人主页](https://haoxiong.wang)

    - 邮箱：[wanghaoxiong@zju.edu.cn](mailto:<wanghaoxiong@zju.edu.cn>)





</div>




   <body>
      <font color="#B9B9B9">
      <p style="text-align: center; ">
              <span>本站已经运行</span>
              <span id='box1'></span>
              <span>最后更新：2026-09-03</span>
      </p>
      <div id="box1"></div>
      <script>
        function timingTime(){
          let start = '2025-2-1 09:00:00'
          let startTime = new Date(start).getTime()
          let currentTime = new Date().getTime()
          let difference = currentTime - startTime
          let m =  Math.floor(difference / (1000))
          let mm = m % 60  // 秒
          let f = Math.floor(m / 60)
          let ff = f % 60 // 分钟
          let s = Math.floor(f/ 60) // 小时
          let ss = s % 24
          let day = Math.floor(s  / 24 ) // 天数
          return day + "天" + ss + "时" + ff + "分" + mm +'秒'
        }
        setInterval(()=>{
          document.getElementById('box1').innerHTML = timingTime()
        },1000)
      </script>
      </font>
    </body>

