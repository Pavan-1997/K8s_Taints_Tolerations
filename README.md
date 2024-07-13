# K8s_Taints_Tolerations

---

```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

`kind create cluster --name=pavantest --config=cluster.yaml`

`k taint node pavantest-worker gpu=true:NoSchedule`

`k taint node pavantest-worker2 gpu=true:NoSchedule`

`k describe node pavantest-worker | grep -i taint`

![image](https://github.com/user-attachments/assets/3506e98b-078b-45b5-b38f-d8ed874bfba1)

`k run nginx --image=nginx`

`k get pods -w`

![image](https://github.com/user-attachments/assets/1f1bca92-ebf3-4131-87a1-a5dcb20022e2)

`k describe pod nginx`

![image](https://github.com/user-attachments/assets/83f582b9-a031-4eaa-b5e7-1450b5cf9ba0)

`k run redis --image=redis --dry-run=client -o yaml > redis.yaml`

In this File we add Tolerations as the one updated in GitHUb

`k apply -f redis.yaml`

`k get pods -w`

![image](https://github.com/user-attachments/assets/bae83f0c-e5bf-467c-9b9c-3ffebcd5d625)

`k get pods -o wide`

![image](https://github.com/user-attachments/assets/7a15a949-4a17-4392-bd3e-bccded8650e0)

Removing the Taint on Node2 for scheduling the Nginx pod

`k taint node pavantest-worker2 gpu=true:NoSchedule-`

Now the Nginx pod is running 

`k get pods -w`

![image](https://github.com/user-attachments/assets/3e830ae9-9ed5-4d8e-8b51-c0bd1bb855fa)

`k get pods -o wide`

![image](https://github.com/user-attachments/assets/ce8fed22-fbbf-460f-b687-f900df94d8d7)

---

## Labels

`k run nginx-new --image=nginx --dry-run=client -o yaml > nginx-new.yaml`

In this File we add Labels as the one updated in GitHUb

![image](https://github.com/user-attachments/assets/d38230b5-803a-433a-9aca-06af7962f614)

`k describe pod nginx-new`

![image](https://github.com/user-attachments/assets/a67eb748-846e-4896-948d-6ac32dc888f4)

`k label node pavantest-worker gpu=false`

`k get pods`

![image](https://github.com/user-attachments/assets/143f71b9-c902-433f-b8d8-ac9efea8326f)

`k get pods -o wide`
 
![image](https://github.com/user-attachments/assets/5a5a0b0a-45d3-44c0-adfb-fc3f9c9be4fc)


