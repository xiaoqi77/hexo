---
title: jQuery动态添加树形结构菜单 Demo
tags: tech
categories: tech
notshow: true
date: 2016-03-24 09:55:13
---

效果图如下：
![效果](menuList.png)

源代码：

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>动态添加树形菜单</title>
	    <script type="text/javascript" src="../jquery.js"></script>
	</head>
	<style type="text/css">
	    .orgMenu ul,.orgMenu li{
	        list-style:none;
	        font-size:14px;
	        margin:0;
	        padding-left:6px;
	        line-height: 30px;
	        color: black;
	    }
	    .child{
	        display:none;
	    }
	    .orgMenu a{
	        display:inline;
	        /*color:black;//#5c84c1;*/
	        padding-left:12px;
	    }
	    .orgMenu li.active{
	        position: relative;
	        background: url(libg.png) no-repeat;
	        /*line-height: 30px;*/
	        color: #fff;
	    }
	    .orgMenu .active>a:first-child{
	        color: #fff;
	    }
	    .orgMenu .treeMenu img{
	        padding: 0px 2px 0px 2px;
	        position: relative;
	        top: 3px;
	    }
	</style>
	<!--more-->
	<script>
	    $(function () {
	        var menuList = ["菜单0","菜单1","菜单2"];
	        function addMenu(orgId){
	            if(orgId != "orgMenu"){
	                for(var i in menuList){
	                    var idOrName = orgId+i;
	                    var  liStr = "<li id='"+idOrName+"'><a href='#' class='treeMenu'>"+idOrName+"</a></li>";
	                    $(liStr).appendTo($("#"+orgId+" ul:first"));
	                    $(document).on("click","#"+idOrName+" a:first", function () {
	                        var liId = $(this).parent().attr("id");
	                        if($("#"+liId).find("ul li").length == 0){
	                            addMenu(liId);
	                        }
	                    });
	                    var ulStr = "<ul class='child'></ul>";
	                    $(ulStr).appendTo($("#"+idOrName));
	                    clickEvent(idOrName,"orgMenu");
	                }
	            }else{
	                for(var i in menuList){
	                    var  liStr = "<li id='"+menuList[i]+"'><a href='#' class='treeMenu'>"+menuList[i]+"</a></li>";
	                    $(liStr).appendTo($("#"+orgId+" ul:first"));
	                    $(document).on("click","#"+menuList[i]+" a:first", function () {
	                        var liId = $(this).parent().attr("id");
	                        if($("#"+liId).find("ul li").length == 0){
	                            addMenu(liId);
	                        }
	                    });
	                    var ulStr = "<ul class='child'></ul>";
	                    $(ulStr).appendTo($("#"+menuList[i]));
	                    clickEvent(menuList[i],"orgMenu");
	                }
	            }
	        }
	        addMenu("orgMenu");
	        clickEvent("orgMenu","orgMenu");
	        //添加click事件
	        function clickEvent(liId,menuClass){
	            $("#"+liId).not(":has(ul)").children("a").css({textDecoration:"none",background:"none"})
	                    .click(function(){
	                        //.one("click",function(){
	                        $("."+menuClass+" li").removeClass("active");
	                        $(this).parent("li").addClass("active");
	                    });
	            if($("#"+liId).find("ul").length != 0){
	                $("#"+liId).children("a:first").css({background:"url(list.gif) no-repeat left center"})
	                        .click(function(e){
	                            //.one("click",function(){
	                            $("."+menuClass+" li").removeClass("active");
	                            $(this).parent("li").addClass("active");
	                            if($(this).next("ul").is(":hidden")){
	                                $(this).next("ul").slideDown("slow");
	                                if($(this).parent("li").siblings("li").children("ul").is(":visible")){
	                                    $(this).parent("li").siblings("li").find("ul").slideUp("1000");
	                                    $(this).parent("li").siblings("li:has(ul)").children("a").css({background:"url(list.gif) no-repeat left center"})
	                                            .end().find("li:has(ul)").children("a").css({background:"url(list.gif) no-repeat left center"});
	                                }
	                                $(this).css({background:"url(clist.png) no-repeat left center"});
	//                            return false;
	                            }else{
	                                $(this).next("ul").slideUp("normal");
	//不用toggle()的原因是为了在收缩菜单的时候同时也将该菜单的下级菜单以后的所有元素都隐藏
	                                $(this).css({background:"url(list.gif) no-repeat left center"});
	                                $(this).next("ul").children("li").find("ul").fadeOut("normal");
	                                $(this).next("ul").find("li:has(ul)").children("a").css({background:"url(list.gif) no-repeat left center"});
	//                            return false;
	                            }
	                        });
	            }
	        }
	    });
	</script>
	<body>
	    <div class="orgMenu" style="clear: both">
	        <ul>
	            <li id="orgMenu">
	                <a href="#" style="font-size: 16px;font-weight: bolder">
	                    组织列表</a>
	                <ul class='child'></ul>
	            </li>
	        </ul>
	    </div>
	</body>
	</html>
