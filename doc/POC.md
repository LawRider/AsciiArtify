# Встановлення argocd

   Встановлення кластеру Kubernetes за допомогою k3d

   Створюємо кластер argo і воркер у ньому:

   ```bash
   k3d cluster create argo
   k3d node create worker -c argo
   ```

   Створюємо неймспейс для ArgoCD:

   ```bash
   kubectl create namespace argocd
   ```

   Встановлюємо ArgoCD з офіційного маніфесту:

   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

   Отримуємо перелік сервісів ArgoCD:

   ```bash
   kubectl get svc -n argocd
   ```

   Маємо отримати наступне:

   ```bash
   NAME                                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
   argocd-applicationset-controller          ClusterIP   10.43.144.69    <none>        7000/TCP,8080/TCP            99m
   argocd-dex-server                         ClusterIP   10.43.112.191   <none>        5556/TCP,5557/TCP,5558/TCP   99m
   argocd-metrics                            ClusterIP   10.43.107.182   <none>        8082/TCP                     99m
   argocd-notifications-controller-metrics   ClusterIP   10.43.144.175   <none>        9001/TCP                     99m
   argocd-redis                              ClusterIP   10.43.18.48     <none>        6379/TCP                     99m
   argocd-repo-server                        ClusterIP   10.43.174.122   <none>        8081/TCP,8084/TCP            99m
   argocd-server                             ClusterIP   10.43.162.18    <none>        80/TCP,443/TCP               99m
   argocd-server-metrics                     ClusterIP   10.43.180.159   <none>        8083/TCP                     99m
   ```

   Щоб отримати доступ до веб-інтерфейсу, потрібно зробити форвардінг портів на argocd-server:

   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443&
   ```

   Відкриваємо ArgoCD у браузері https://127.0.0.1:8080

   ![Логін-форма ArgoCD](https://github.com/LawRider/AsciiArtify/blob/main/doc/img/argocd-login.jpg)

   Логін ім'я для входу - admin, а пароль можна отримати з секрету:

   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"|base64 -d; echo
   ```

   Після логіну бачимо наступний інтерфейс:
   
   ![Інтерфейс ArgoCD](https://github.com/LawRider/AsciiArtify/blob/main/doc/img/argocd.jpg)
