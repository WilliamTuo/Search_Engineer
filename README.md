
<html>
<body>
<a name="1458"/>
<h1>项目简介</h1>
<div>
  <span>
    <div>一、问题背景</div>
    <div>
      boost 开源库文档内容很多，但又不方便快速查找到某些组件，实现一个针对 boost 库文档的搜索引擎。
    </div>
    <div><br/></div>
    <div>二、模块 + 流程<br/></div>
    <div>1.四个模块</div>
    <div>
      http 服务器模块（http_server）、CGI 程序（搜索引擎的客户端）、搜索服务器（TCP + RPC）、索引模块（核心数据结构）
    </div>
    <div>    </div>
    <div>
      2.核心流程
    </div>
    <div>
      1.浏览器发送一个 HTTP 请求（核心参数， query）给 HTTP 服务器
    </div>
    <div>
      2.HTTP 服务器解析 HTTP 请求，交给 CGI 程序进行处理
    </div>
    <div>
     3. CGI 程序 query 包装成 TCP 的请求发送给搜索服务器
     </div>
     <div>
     4.搜索服务器进行检索操作
     </div>
     <div>
     5.把结果返回给 CGI 程序
     </div>
     <div>
     6.CGI 程序把结果包装成 HTML ，由 HTTP 服务器返回给浏览器
     </div><div><br/></div>
     <div>三、项目组织结构<br/></div>
     <div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">
      1.数据处理模块
      </span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">        索引制作之前，需要对输入数据进行脱标签操作（去掉 html 标签）： 基于 python 实现 （正则去标签）</span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">        把 html 目录中的所有的文件进行遍历，读取文件内容并且去标签。得到的结果组织成一个三元组（url, title, cotent）。三元组作为输出的 raw_input 文件中的一行。三元组之间用 \3 来分割。</span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><br style="box-sizing: border-box;"/></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">    2.索引模块</span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">        索引制作程序读取 raw_input 文件，进行制作索引，生成索引文件</span><span style="font-size: medium;">（index_file） 放到 ouput 目录中。</span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">        在内存中构建出结构化的数据，需要保存到文件之中，供后面的服务器进行加载。</span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">        加载和保存需要序列化 和 反序列化。</span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">    </span></div><div style="box-sizing: border-box; margin: 0px; padding: 0px; font-size: medium; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px;"><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">    3.搜索模块</span></div><div><span style="box-sizing: border-box; font-size: medium; letter-spacing: normal; orphans: 2; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; color: rgb(0, 0, 0); font-family: 微软雅黑; font-variant-caps: normal; font-variant-ligatures: normal;">        根据用户输入的查询词，对索引进行查找，最终找到词与哪些文档有关。</span></div><div><br/></div>
      <div>四、搜索服务器核心流程</div>
      <div>    1.对请求进行解析</div>
      <div>    2.对查询词进行分词 cppjieba</div>
      <div>    3.触发（retrieve）针对每个分词结果找到都有哪些网页和这个词具有相关性，项目词在网页（文档）中出现的次数越高，相关性就越高</div>
      <div>    4.排序（rank） 按照相关程序降序排序（获取到了一组文档 id）</div>
      <div>    5.根据文档 id，来获取到文档的详细内容（标题，描述...）</div>
      <div>    6.构造响应，写回给客户端</div><div><br/></div><div><br/></div></span>
</div></body></html>
