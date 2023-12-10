# Демонстрація роботи додатку розгорнутого за допомогою ArgoCD

   Створюємо додаток в інтерфейсі ArgoCD
   
   ![Додаток ArgoCD](https://github.com/LawRider/AsciiArtify/blob/main/doc/img/argocd-app.jpg)

   Щоб отримати доступ до додатку, потрібно зробити форвардінг портів на нього:

   ```bash
   kubectl port-forward svc/ambassador -n demo 8088:80&
   ```
   Зберігаємо локально зображення, яке буде передано додатку на обробку:

   ```bash
   wget -O /tmp/t.png https://prometheus.org.ua/wp-content/uploads/2022/04/cropped-favicon_yellow_blue-2-192x192.png
   ```
   
   Передаємо зображення додатку:
   
   ```bash
   curl -F 'image=@/tmp/p.png' localhost:8088/img/
   ```

   Отримуємо оброблене зображення у відповідь:
   ![Результат роботи додатку ArgoCD](https://github.com/LawRider/AsciiArtify/blob/main/doc/img/argocd-app-result.jpg)
