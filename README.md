
## Deployment

Proje reposunun çekileceği ortamda ```.kube/config ``` dosyasına kurulum yapılacak k8s cluster bilgileri eklenmelidir .Daha sonra kubectx ile ilgili clustera geçilmelidir .



```bash
  kubectx k8s-cluster-name
```

Proje için self-signed sertifika oluşturulacaksa aşağıdaki komut ile oluşturulup projenin ```roles/common/templates ```
dizinine eklenmelidir .

```bash
  openssl req \
-x509 -newkey rsa:4096 -sha256 -nodes \
-keyout tls.key -out tls.crt \
-subj "/CN=galaksiya-k8s.local" -days 365

```
Proje domain bilgilerini değiştirmek için ```roles/common/vars/main.yaml ``` dosyasını editlemek yeterlidir .

```bash
---
nexus:
  host:
    Name: 
    Path: 
  tls:
    Name: 
    CrtName: 
    KeyName: 
keycloak:
  host:
    Name: 
    Path: 
  tls:
    Name: 
    CrtName: 
    KeyName: 

```

Eğer yukarıdaki bilgiler düzgün ayarlandıysa aşağıdaki şekilde uygulamalar clusterda ayaklandırılır .

```bash
  ansible-playbook  site.yml

```