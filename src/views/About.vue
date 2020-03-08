<template>
  <div class="about">
    <h2>
      三、 前端工程化的处理方式
    </h2>
    <h3>
      a) 如何进行工程化？
    </h3>
    <h4>
      提升前端开发效率，提高前端应用质量的手段和工具。比如使用 Webpack 解决接口 mock、代码检查、代码编译、构建、压缩、添加版本号、部署等
    </h4>
    <h3>
     b) 如何进行多人并行开发？
    </h3>
    <h4>
     使用git开发
    </h4>
    <h3>
    c) 如何设置质量控制点？
    </h3>
    <h4>
     进行单元测试
    </h4>
    <h3>
    d) 开发过程中，可使用哪些工具？
    </h3>
    <h4>
    git、vscode、axure、photoshop、webstorm
    </h4>
   <h2>
      四、 前端的移动化多平台打包的思路，如何实现一套代码多个平台使用？
    </h2>
    <h3>
     使用uniapp
    </h3>
     <h2>
      五、 跨域的原因及主要解决的思路。
    </h2>
    <h3>
     跨域的原因：关闭会容易受到XSS和CSRF的攻击
    </h3>
     <h3>
     解决思路：
    </h3>
     <h3>
     1、js可以使用jsonp进行跨域
    </h3>
     <h3>
     2、通过修改document.domain来跨子域
    </h3>
     <h3>
     3、使用window.name来进行跨域
    </h3>
     <h3>
     4、window.postMessage进行跨域
    </h3>
    <h2>
      六、 一棵树在DB中，如何表达?
    </h2>
    <h3>
    有个根节点，存储每个元素他的父节点ID
    </h3>
    <h2>
      七、 多对多如何在数据库中进行表达？
    </h2>
    <h3>
    新建一个关系表，将两张表关系起来。关系表中是两张表的主键
    </h3>
    <h2>
      八、 使用Js代码，写出一个针对树的 先根遍历算法。
    </h2>
    <h3>
      <pre>
        function treeMethod(tree){
          console.log(tree.value);
          if(tree.left){
              treeMethod(tree.left);
          }
          if(tree.right){
              treeMethod(tree.right);
          }
        }
      </pre>
    </h3>
    <h2>
     九、 http协议的报头含义？
    </h2>
    <h3>
    HTTP协议报文组成部分:请求报文、响应报文
    </h3>
    <h3>
    请求报文：请求行，请求头、空行、请求体
    </h3>
    <h3>
   请求行：http方法+页面地址+http协议+版本
    </h3>
    <h3>
    请求头（key,value值）一些提交给服务器关于客户端的基本信息
    </h3>
    <h3>
    响应报文：状态行，响应头，空行，响应体
    </h3>
    <h2>
     十、 采用VUE编码的时候，页面上按钮的权限控制思路？
    </h2>
    <h3>
    首先获取按钮的权限标识，判断是否存在，若存在为true，否则为false，用v-if进行控制按钮的权限，是否显示。
    </h3>
     <h2>
     十一、 如何实现前端页面的自适应？
    </h2>
    <h3>
      1、flex布局、2、栅格系统、3、@media
    </h3>
    <h3>
      <pre>
        @media screen and (max-width: 450px){
            .container{
                background: red;
            }
        }
      </pre>
    </h3>
     <h2>
     十二、 提升前端页面的性能有哪些方式？
    </h2>
    <h3>
      1. JavaScript 压缩和模块打包      2. 按需加载资源      3. 缓存      4. 使用索引加速数据库查询    
  5. 使用更快的转译方案      6. 避免或最小化 JavaScript 和 CSS 的使用而阻塞渲染      7. 图片编码优化
    </h3>
 </div>
</template>
<style>
 .about{
   text-align:left;
   padding:0 200px;
 }
</style>
