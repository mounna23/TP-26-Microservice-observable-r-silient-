# TP 26 : Microservice observable & résilient avec MySQL + Actuator + Profiles + Wait Strategy + Resilience4j + Multi-instances
## Dans ce TP
On va construire 2 microservices :

- pricing-service
- - Un petit service qui renvoie un prix. Il peut “tomber en panne” volontairement pour tester la robustesse.
book-service
- - Un service qui gère des livres (titre, auteur, stock) dans une base MySQL.
- - Quand on emprunte un livre, book-service :
- - - décrémente le stock en base
- - - appelle pricing-service pour récupérer un prix
si pricing-service est en panne, book-service ne doit pas planter ⇒ il doit continuer avec un fallback.
- - Ensuite on déploie tout dans Docker Compose :

- - - une base MySQL (avec volume pour garder les données)
- pricing-service
- - - 3 instances de book-service (comme en production)
- - - et on met une wait strategy pour éviter que book-service démarre avant MySQL (erreur classique).
