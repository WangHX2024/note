---
hide:
  - footer
  - feedback
title: 主页
---

<center><font  color= #518FC1 size=6>王浩雄的个人主页</font>

<p><font color="#B9B9B9">记住我的名字，就不会忘记这个网站的地址 <b>https://note.haoxiong.wang</b></font></p>
</center>

<div class="grid cards" markdown>

-   :fontawesome-solid-code:{ .lg .middle } __提示__

    ---

    课程笔记正在实时更新中~ 请移步 [Notion](https://classnote.haoxiong.wang) 查看详情~


</div>

<div class="grid cards" markdown>

-   :material-book-open-variant-outline:{ .lg .middle } __推荐阅读__

    ---


    - [x] [数字逻辑设计](/note/2024-2025 春夏课程笔记 19d9c6b6155b80e2bfcad2e0753bfbda/数字逻辑设计 19b9c6b6155b806c8644e4a55f0b8dfb)

    - [ ] [计算机体系结构](/note/2024-2025 春夏课程笔记 19d9c6b6155b80e2bfcad2e0753bfbda/计算机体系结构 19b9c6b6155b8024a072ca3bd97e46c8)

    - [ ] [数据库系统](/note/2024-2025 春夏课程笔记 19d9c6b6155b80e2bfcad2e0753bfbda/数据库系统 19b9c6b6155b80d695c5ec0cf8168783)

    - [ ] [面向对象程序设计](/note/2024-2025 春夏课程笔记 19d9c6b6155b80e2bfcad2e0753bfbda/面向对象程序设计 19b9c6b6155b80459f10d6623d7c42e7)

    - [ ] [离散数学](/note/2024-2025 春夏课程笔记 19d9c6b6155b80e2bfcad2e0753bfbda/离散数学 19b9c6b6155b80108585d9246eeefe70)


-   :fontawesome-solid-user-tag:{ .lg .middle } __关于我__

    ---
    
    - 王浩雄同学来自**河北秦皇岛市**，现为浙江大学竺可桢学院混合班2023级本科生，主修专业为**计算机科学与技术**。

    - 电话：+86-15703396384

    - 邮箱：wanghaoxiong@zju.edu.cn

    - 地址：浙江省杭州市西湖区浙大路38号 310000



</div>




   <body>
      <font color="#B9B9B9">
      <p style="text-align: center; ">
              <span>本站已经运行</span>
              <span id='box1'></span>
              <span>最后更新：2025/8/25</span>
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

