---
title: jquery取得select选择的文本与值 
tags: tech
categories: tech
notshow: true
date: 2016-03-28 10:54:34
---

jquery获取select选择的文本与值
获取select ：
获取select 选中的 text :
    $("#ddlregtype").find("option:selected").text();

获取select选中的 value:
    $("#ddlregtype ").val();

获取select选中的索引:
    $("#ddlregtype ").get(0).selectedindex;

设置select:
设置select 选中的索引：
    $("#ddlregtype ").get(0).selectedindex=index;//index为索引值

设置select 选中的value：
    $("#ddlregtype ").attr("value","normal“);
    $("#ddlregtype ").val("normal");
    $("#ddlregtype ").get(0).value = value;

设置select 选中的text:

    var count=$("#ddlregtype option").length;
      for(var i=0;i<count;i++)
         {           if($("#ddlregtype ").get(0).options[i].text == text)
            {
                $("#ddlregtype ").get(0).options[i].selected = true;
                break;
            }
        }
    $("#select_id option[text='jquery']").attr("selected", true);

设置select option项:

    $("#select_id").append("<option value='value'>text</option>");  //添加一项option
    $("#select_id").prepend("<option value='0'>请选择</option>"); //在前面插入一项option
    $("#select_id option:last").remove(); //删除索引值最大的option
    $("#select_id option[index='0']").remove();//删除索引值为0的option
    $("#select_id option[value='3']").remove(); //删除值为3的option
    $("#select_id option[text='4']").remove(); //删除text值为4的option

清空 select:

    $("#ddlregtype ").empty();

工作需要，要获得两个表单中的值。如图：

如何获得从左边选择框添加到右边选择框中的值？我想了想用网页特效可以获得，这里用了比较流行的jquery。
js代码如下：

    //获取所有属性值 var item = $("#select1").val();
    $(function(){
      $('#select1').each(  //获得select1的所有值
         function(){
            $('button').click(function(){
                alert($('#select2').val());  //获得select2中的select1值
            });
         });
    })
    </script>

值得注意的是，不能直接写成

    $(function(){
      $('#select2').each(  //获得select1的所有值，因为前面讲选项从左边添加到右边，jquery其实并没有真正将值从左边传到右边。
         function(){
            $('button').click(function(){
                alert($(this).val());  //获得select2中的select1值
            });
         });
    })

html 源码：

	<div class="centent">
	        <select multiple="multiple" id="select1" name="dd" style="width:100px;height:160px;">
	            <option value="1">选项1</option>
	            <option value="2">选项2</option>
	            <option value="3">选项3</option>
	            <option value="4">选项4</option>
	            <option value="5">选项5</option>
	            <option value="6">选项6</option>
	            <option value="7">选项7</option>
	        </select>
	        <div>
	            <span id="add" >选中添加到右边&gt;&gt;</span>
	            <span id="add_all" >全部添加到右边&gt;&gt;</span>
	        </div>
	    </div>
	    <div class="centent">
	        <select multiple="multiple" id="select2" name="sel" style="width: 100px;height:160px;">
	        </select>
	        <div>
	            <span id="remove">&lt;&lt;选中删除到左边</span>
	            <span id="remove_all">&lt;&lt;全部删除到左边</span>
	        </div>
	    </div>

使用JQuery，Ajax调用动态填充Select的option选项

    //绑定ClassLevel1单击事件
        $("#ClassLevel1").change(function () {
            var id = $("#ClassLevel1").val();
            var level2 = $("#ClassLevel2");
            level2.empty();
            $("#ClassLevel3").hide();
            $.ajax({
                url: "./askCommon.ashx?action=getclasslevel&pid=" + id,
                data: { "type": "ajax" },
                datatype: "json",
                type: "get",
                success: function (data) {
                    var json = eval_r(data);
                    for (var ind in json) {
                        level2.append($("<option value='" + json[ind].id + "'>" + json[ind].typename + "</option>"));
                    }
    
                }
            });
        })
