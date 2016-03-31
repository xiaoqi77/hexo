---
title: 创建XHR对象
tags: tech
categories: tech
notshow: true
date: 2016-03-30 16:09:41
---

var xmlHttp;
try {
        xmlHttp = new XMLHttpRequest();
    } catch (e) {
        var aTypes = ['Microsoft.XMLHTTP', 'MSXML.XMLHTTP', 'Msxml2.XMLHTTP.7.0','Msxml2.XMLHTTP.6.0',
            'Msxml2.XMLHTTP.5.0', 'Msxml2.XMLHTTP.4.0', 'MSXML2.XMLHTTP.3.0', 'MSXML2.XMLHTTP'];
        var len = aTypes.length;
        for (var i = 0; i < len; i++) {
            try {
                xmlHttp = new ActiveXObject(aTypes[i]);
            } catch (e) {
                continue;
            }
            break;
        }
    }
