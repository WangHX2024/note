---
hide:
  - footer
  - feedback
title: 主页
---

<center><font  color= #518FC1 size=6>王浩雄的个人主页</font>

<p><font color="#B9B9B9">记住我的名字，就不会忘记这个网站的地址 <b>https://haoxiong.wang</b></font></p>
</center>

<div class="grid cards" markdown>

-   :fontawesome-solid-code:{ .lg .middle } __提示__

    ---

    本网站正在加紧施工中~ 期待有朝一日网站正式开放~

</div>

<div class="grid cards" markdown>

-   :material-book-open-variant-outline:{ .lg .middle } __推荐阅读__

    ---

    - [Markdown 学习笔记](/note/Markdown Extensions)

    - [LaTeX 学习笔记](/note/LaTeX学习笔记)

    - [C# 学习笔记](/note/C#学习笔记)



-   :fontawesome-solid-user-tag:{ .lg .middle } __关于我__

    ---
    王浩雄同学来自河北秦皇岛市，现就读于浙江大学竺可桢学院混合2303班，主修专业为计算机科学与技术。



</div>




   <body>
        <font color="#B9B9B9">
        <p style="text-align: center; ">
                <span>本站已经运行</span>
                <span id='box1'></span>
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


