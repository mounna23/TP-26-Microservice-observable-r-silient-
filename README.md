# TP 26 : Microservice observable & résilient avec MySQL + Actuator + Profiles + Wait Strategy + Resilience4j + Multi-instances
## Dans ce TP
On va construire 2 microservices :

- pricing-service
- - Un petit service qui renvoie un prix. Il peut “tomber en panne” volontairement pour tester la robustesse.
book-service
  - Un service qui gère des livres (titre, auteur, stock) dans une base MySQL.
  - Quand on emprunte un livre, book-service :
    - décrémente le stock en base
    - appelle pricing-service pour récupérer un prix
si pricing-service est en panne, book-service ne doit pas planter ⇒ il doit continuer avec un fallback.
  - Ensuite on déploie tout dans Docker Compose :

   - une base MySQL (avec volume pour garder les données)
- pricing-service
    - 3 instances de book-service (comme en production)
    - et on met une wait strategy pour éviter que book-service démarre avant MySQL (erreur classique).
## pricing-service (Web + Actuator)
<img width="1470" height="956" alt="Capture d’écran 2025-12-24 à 18 35 00" src="https://github.com/user-attachments/assets/7a520c77-6054-40e1-9d1b-101ab9dc4bee" />
<img width="1470" height="956" alt="Capture d’écran 2025-12-24 à 18 35 19" src="https://github.com/user-attachments/assets/b5a55bad-08be-480e-8add-0716a425c49d" />
<img width="1470" height="956" alt="Capture d’écran 2025-12-24 à 18 35 42" src="https://github.com/user-attachments/assets/e3e07c6d-6a25-4941-abfa-e886e0396fd2" />
<img width="1470" height="956" alt="Capture d’écran 2025-12-24 à 18 35 59" src="https://github.com/user-attachments/assets/ee44d6e3-66f5-4eb0-8a15-868aa5325e7a" />
## book-service (Web + JPA + MySQL + H2 + Actuator + Resilience4j)
## Test local 
<img width="1452" height="187" alt="Capture d’écran 2025-12-25 à 14 06 26" src="https://github.com/user-attachments/assets/4d2032d6-ae45-4e11-92c7-7ef9e6909929" />
<img width="1452" height="217" alt="Capture d’écran 2025-12-25 à 14 09 13" src="https://github.com/user-attachments/assets/12540e27-a2c1-44b5-a159-caddc5c7974f" />
## Docker Compose
<img width="2940" height="1838" alt="image" src="https://github.com/user-attachments/assets/90eab985-bf6b-40dc-a2cf-8adb84e02e21" />
## Scénarios de validation 
<img width="2904" height="434" alt="image" src="https://github.com/user-attachments/assets/cae1088a-308c-49a0-b544-1d79b81f667f" />
