# kubernetes-cheat-sheet


# Nodes

1-) Node'ların listelenmesi

```kubectl get nodes``` ve(ya) ```kubectl get no```

### Not: Diğer örneklerde de göreceğiniz gibi, bazı parametreler varsayılan olarak kısaltmalara sahiptir. İki kullanımın output olarak herhangi bir farkı yoktur.


<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/1.png" width="450">

Aynı komut "-o wide" parametresiyle birlikte kullanıldığında Internal-External IP, işletim sistemi, çekirdek versiyonu ve Docker Runtime bilgileri de gösterilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/3.png" width="450">

"--show-labels" parametresi ile label bilgileri görüntülenebilir. Bu parametreden aldığınız sonucu "--selector" parametresi ile birlikte kullanarak "label" bazlı listeleme yapabilirsiniz.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/16.png" width="450">

Listeme işlemlerinde JSON bazlı filtrelemeler de yapılabilmektedir. Örneğin sadece Internal IP bilgilerini getirmek için:

```kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="InternalIP")].address}'```

gibi bir kullanım mümkündür.


2-) Node'lar hakkında bilgi alma

```kubectl describe nodes``` ve(ya) ```kubectl describe no```

Herhangi bir node adı belirtilmediğinde mevcut cluster üzerinde çalışan tüm node'lar sırasıyla listelenir. Argüman olarak bir node adı verildiğinde ise o node'a ait detaylı bilgiler görüntülenir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/2.png" width="450">


Bir node hakkında çok daha ayrıntılı bilgi alabilmek için "get" ile birlikte "-o yaml" parametresi de kullanılabilir. Bu şekilde bilgiler JSON formatında aktarılır.

```kubectl get no -o yaml```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/4.png" width="450">

3-) Node üzerinde değişiklik yapma

```kubectl edit no node_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/32.png" width="450">

# Pods

1-) Yeni Pod oluşturma

```kubectl create -f dosya_adı``` ve(ya) ```kubectl apply -f dosya_adı```

### Not: create "Imperative", apply "Declarative" mantığıyla çalışır.

Pod oluşturulurken mevcut YAML dosyası kullanlabileceği gibi "run" ve belirleyici diğer parametreler ile birlikte de aynı işlem gerçekleştirilebilir.

```kubectl run pod_adı --image=redis```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/27.png" width="450">


2-) Pod'ların listelenmesi

```kubectl get pods``` ve(ya) ```kubectl get po```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/5.png" width="450">

"-o wide" kullanımı pod'lar için de geçerlidir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/6.png" width="450">

"--show-labels" kullanımı burada da geçerlidir. Label bilgisine göre "-l" parametresi ile filtreleme yapılabilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/17.png" width="450">


3-) Pod'lar hakkında bilgi alma

```kubectl describe pods``` ve(ya) ```kubectl describe po```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/7.png" width="450">

Pod adı belirtilmediği sürece tüm pod'ların bilgisi listelenir. Özellikle troubleshooting gerektiren durumlarda ilk başvurulan komutlardan birisidir.

4-) Pod'ların silinmesi

```kubectl delete pods``` ve(ya) ```kubectl delete po```

Çoklu silmeler için Pod isimleri aralarında boşluk bırakalarak tanımlanabilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/28.png" width="450">

5-) Pod üzerinde değişiklik yapma

```kubectl edit po pod_adı```

6-) Pod'u interaktif modda başlatma

```kubectl run -i --tty busybox --image=busybox -- sh```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/44.png" width="450">

7-) Yeni başlatılan Pod'un özelliklerini YAML formatında dosyaya aktarma

```kubectl run pod_adı --image=alpine -o yaml > my_pod.yaml```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/45.png" width="450">

8-) Pod üzerinde komut çalıştırma

```kubectl exec pod_adı -- komut```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/46.png" width="450">

# Namespaces

1-) Yeni namespace oluşturma

```kubectl create namespace namespace_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/29.png" width="450">

2-) Namespace'lerin listelenmesi

```kubectl get namespaces``` ve(ya) ```kubectl get ns```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/8.png" width="450">

"-o yaml" parametresi namespace'ler için de aktiftir.

3-) Namespace'ler hakkında bilgi alma

```kubectl describe namespaces``` ve(ya) ```kubectl describe ns```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/9.png" width="450">

4-) Namespace'lerin silinmesi

```kubectl delete namespace namespace_adı``` ve(ya) ```kubectl delete ns namespace_adı```


# Deployments

1-) Yeni Deployment oluşturma

```kubectl create deployment deployment_adı --image=imaj_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/30.png" width="450">


2-) Deployment'ların listelenmesi

```kubectl get deployments``` ve(ya) ```kubectl get deploy```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/10.png" width="450">

Kullanılan Docker imajları ve "selector" bilgisi "-o wide" ile görüntülenebilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/11.png" width="450">


"-o yaml" parametresi aynı şekilde Deployment'lar için de kullanılabilir.

3-) Deployment'lar hakkında bilgi alma

```kubectl describe deployments``` ve(ya) ```kubectl describe deploy```

Yine troubleshoot durumlarında kullanılan başlıca komutlardan birisidir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/12.png" width="450">

4-) Deployment'ların silinmesi

```kubectl delete deployments deployment_adı``` ve(ya) ```kubectl delete deploy deployment_adı```


# Services

1-) Yeni Service oluşturma

```kubectl create service loadbalancer mylb --tcp="80:8080"```

Ana şablon "kubectl create service" ile başlar, sonrasında service tipi belirtilmelidir. Bu örnekte "loadbalancer" tipi seçilmiştir. Diğer tipler:

- clusterip
- externalname
- nodeport

Sonrasında service adı ve port tanımlanır.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/31.png" width="450">


2-) Service'lerin listelenmesi

```kubectl get services``` ve(ya) ```kubectl get svc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/13.png" width="450">

"-o wide" parametresi "selector" bilgisini getirir. "-o yaml" kullanımı servisler için de geçerlidir.

"--show-labels" parametresi ile servise atanan label bilgileri de görüntülenebilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/15.png" width="450">


3-) Service'ler hakkında bilgi alma

```kubectl describe services service_adı``` ve(ya) ```kubectl describe svc service_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/14.png" width="450">

4-) Service üzerinde değişiklik yapma

```kubectl edit service``` ve(ya) ```kubectl edit svc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/35.png" width="450">

5-) Service'lerin silinmesi

```kubectl delete services service_adı``` ve(ya) ```kubectl delete svc service_adı```


# DaemonSet

1-) DaemonSet'lerin listelenmesi

```kubectl get daemonset``` ve(ya) ```kubectl get ds```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/18.png" width="450">


2-) DaemonSet hakkında bilgi alma

```kubectl describe daemonset``` ve(ya) ```kubectl describe ds```

3-) DaemonSet üzerinde değişiklik yapma

```kubectl edit daemonset``` ve(veya) ```kubectl edit ds```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/36.png" width="450">

4-) DaemonSet'lerin silinmesi

```kubectl delete daemonset daemonsets_adı``` ve(ya) ```kubectl delete ds daemonsets_adı```


# PersistentVolume

1-) PersistentVolume'ların listelenmesi

```kubectl get persistentvolume``` ve(ya) ```kubectl get pv```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/21.png" width="450">

2-) PersistentVolume hakkında bilgi alma

```kubectl describe persistentvolume``` ve(ya) ```kubectl describe pv```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/22.png" width="450">

3-) PersistentVolume'lerin silinmesi

```kubectl delete persistentvolume persistentvolume_adı``` ve(ya) ```kubectl delete pv persistentvolume_adı```


# PersistentVolumeClaim

1-) PersistentVolumeClaim'ların listelenmesi

```kubectl get persistentvolumeclaim``` ve(ya) ```kubectl get pvc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/23.png" width="450">

2-) PersistentVolumeClaim'ler hakkında bilgi alma

```kubectl describe persistentvolumeclaim``` ve(ya) ```kubectl describe pvc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/24.png" width="450">

3-) PersistentVolumeClaim'lerin silinmesi

```kubectl delete persistentvolumeclaim persistentvolumeclaim_adı``` ve(ya) ```kubectl delete pvc persistentvolumeclaim_adı```


# ReplicaSets

1-) ReplicaSets listelenmesi

```kubectl get replicasets``` ve(ya) ```kubectl get rs```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/25.png" width="450">

2-) ReplicaSets hakkında bilgi alma

```kubectl describe replicasets``` ve(ya) ```kubectl describe rs```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/26.png" width="450">

3-) ReplicaSet'lerin silinmesi

```kubectl delete replicaset(s) replicaset_adı``` ve(ya) ```kubectl delete rs replicaset_adı```

# ConfigMaps

1-) ConfigMap'lerin listelenmesi

```kubectl get configmaps``` ve(ya) ```kubectl get cm```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/37.png" width="450">

2-) ConfigMap'ler hakkında bilgi alma

```kubectl describe configmaps configmap_adı``` ve(ya) ```kubectl describe cm configmap_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/38.png" width="450">

# Secrets

1-) Secret'ların listelenmesi

```kubectl get secret``` ve(ya) ```kubectl get secrets```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/39.png" width="450">

# Roles

1-) Rollerin listelenmesi

```kubectl get roles```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/40.png" width="450">

# Events

1-) Event'ların listelenmesi

```kubectl get events``` ve(ya) ```kubectl get ev``` 

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/20.png" width="450">

2-) Event'ların anlık takip edilmesi

```kubectl get events -w``` ve(ya) ```kubectl get ev -w``` 

# Logs

1-) Pod loglarının görüntülenmesi

```kubectl logs pod_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/41.png" width="450">

2-) Son X satır log'ların listelenmesi

```kubectl logs --tail=X pod_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/42.png" width="450">

3-) Son X saatlik - X dakikalık log'ların listelenmesi

```kubectl logs --since=X pod_adı```

Saat bazlı listelemede "h" kullanılır,

Dakika bazlı listelemede "m" kullanılır.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/43.png" width="450">

4-) Belirli bir selector'a sahip pod'lara ait log'ların listelenmesi

```kubectl logs --selector=selector_kriterleri```

Örneğin label olarak `run=main_svc` belirtilmiş pod'larınızın tümünden log çıktısı almak için

```kubectl logs --selector=run=main_svc```

yazabilirsiniz.

# ServiceAccounts

1-) ServiceAccount'ların görüntülenmesi

```kubectl get serviceaccounts``` ve(ya) ```kubectl get sa```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/51.png" width="450">

2-) Bilgilerin .yaml formatında alınması

```kubectl get serviceaccounts -o yaml``` ve(ya) ```kubectl get sa -o yaml```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/52.png" width="450">
 

## Genel Bilgiler ve İpuçları

1-) Component'lar farklı namespace'ler altında oluşturulmuş olabilir, listelemeler varsayılan olarak "default" namespace'i baz alınarak yapılır. Bu tarz durumlarda "-n" parametresi ile hedef namespace belirtilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/19.png" width="450">

2-) Tüm yapıların listelenmesi

```kubectl get all```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/33.png" width="450">

3-) Cluster hakkında temel bilgi alma

```kubectl cluster-info```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/34.png" width="450">

4-) cat komutu ile çoklu component oluşturma

```cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: nightw
spec:
  containers:
  - name: nightw
    image: oraclelinux
    args:
    - sleep
    - "1000"
---
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    args:
    - sleep
    - "1700"
EOF
```

5-) Çoklu component silme

```kubectl delete pod,svc mypod mysrv```

6-) PersistentVolume'ların boyuta göre listelenmesi

```kubectl get pv --sort-by=.spec.capacity.storage```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/47.png" width="450">

7-) Ölçeklendirmenin güncellenmesi

```kubectl scale --replicas=X component_tipi/component_adı```

Resimdeki örnekte 1 replica olarak çalışan deployment 3 replica şeklinde güncellenmiştir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/48.png" width="450">

8-) Container log'larını görüntüleme

```kubectl logs pod_adı -c container_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/49.png" width="450">

9-) Mevcut Pod'a label ekleme

```kubectl label pod pod_adı mein=kampf```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/50.png" width="450">

10-) Bash için otomatik komut tanımlamanın ayarlanması

```source <(kubectl completion bash```

Not: Komutun çalışması için bash-completion paketinin yüklü olması gerekmektedir.

İşlemin kalıcı olması adına .bashrc dosyasına yazmak için:

```echo "source <(kubectl completion bash)" >> ~/.bashrc``` 

11-) Aynı anda birden çok kubeconfig dosyasının kullanılması

config ve config2 isimli dosyalarımız olduğunu varsayalım.

```export KUBECONFIG=~/.kube/config:~/.kube/config2```
