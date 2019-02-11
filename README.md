# 淘宝买家秀

## 添加到浏览器书签

在搜索页面上点击书签会在每一个商品Item下面出现一个按钮

```
javascript:function addHtml(){var api='http://chishenme.ztianzeng.com/?id=';var t=location,e=document,o=encodeURIComponent,c=(t.search.match(/[?&]id=(\d+)/i)||[])[1],n=o(e.title),m=c+'&t='+n;if(c){t.href=api+m}const aa=document.getElementsByTagName("div");for(let i=0;i<aa.length;i++){if(aa[i].getAttribute('data-category')==='auctions'){const para=document.createElement("dev");const href=document.createElement("a");const hrefContent=document.createTextNode('查看买家秀');const elementsByTagName=aa[i].getElementsByTagName('a');let itemId;for(let j=0;j<elementsByTagName.length;j++){if(elementsByTagName[j].getAttribute('data-nid')){itemId=elementsByTagName[j].getAttribute('data-nid')}}href.setAttribute("href",api+itemId);href.setAttribute("target",'view_window');href.appendChild(hrefContent);para.appendChild(href);aa[i].appendChild(para)}}return false}addHtml();
```

## 油猴脚本

~~~

// ==UserScript==
// @name         买家秀
// @version      3.4
// @description  买家秀
// @author       yyyy
// @include      http*://s.taobao.com/*
// @require      https://cdn.bootcss.com/jquery/2.2.4/jquery.min.js
// @grant        none
// ==/UserScript==

(function() {
    var api = 'http://chishenme.ztianzeng.com/?id=';

    $('body').on("DOMNodeInserted", ".item.J_MouserOnverReq", function (event) {
        if($(event.target).attr('class') == 'ww-inline ww-online'){
            var s = $(event.currentTarget).find('a[data-nid]');
            var href = api + s.attr('data-nid');
            if($(event.currentTarget).find('a.zeng').length == 0){
                $(event.currentTarget).find('.ctx-box.J_MouseEneterLeave').append('<a class=zeng target="view_window" href="'+href+'">查看买家秀</p>');
            }

            var adS = $('.item.J_MouserOnverReq.item-ad').find('a[data-nid]');
            if($('.item.J_MouserOnverReq.item-ad').find('a.zeng').length == 0){
                $('.item.J_MouserOnverReq.item-ad').find('.ctx-box.J_MouseEneterLeave').append('<a class=zeng target="view_window" href="'+api+adS.attr('data-nid')+'">查看买家秀</p>');
            }
        }
    });


})();

~~~