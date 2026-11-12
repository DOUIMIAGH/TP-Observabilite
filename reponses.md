# Réponses aux questions de compréhension

## 1. Quelle est la différence entre Prometheus et Grafana ?

Prometheus collecte et stocke les métriques sous forme de séries temporelles. Il permet aussi de les interroger avec PromQL. Grafana utilise ces données pour créer des graphiques et des tableaux de bord.

## 2. Quel est le rôle de Node Exporter ?

Node Exporter expose les métriques système d'une machine Linux, par exemple le CPU, la mémoire, le disque et le réseau. Prometheus récupère ces métriques sur le port 9100.

## 3. Que signifie le terme scraping ?

Le scraping est l'action par laquelle Prometheus interroge régulièrement un endpoint HTTP afin de récupérer ses métriques.

## 4. À quoi sert le fichier `prometheus.yml` ?

Le fichier `prometheus.yml` configure Prometheus. Il définit notamment la fréquence de collecte, les jobs et les targets à superviser.

## 5. Pourquoi Grafana utilise-t-il l'adresse `prometheus:9090` ?

Grafana et Prometheus sont dans le même réseau Docker. Docker permet à Grafana de joindre le conteneur Prometheus avec son nom de service `prometheus`. L'adresse `localhost:9090` désignerait le conteneur Grafana lui-même et non Prometheus.

## 6. À quoi sert PromQL ?

PromQL est le langage de requête de Prometheus. Il sert à sélectionner, filtrer, calculer et agréger les métriques stockées.

## 7. Pourquoi utilise-t-on des volumes Docker ?

Les volumes permettent de conserver les données de Prometheus et de Grafana lorsque les conteneurs sont arrêtés, supprimés ou recréés.

## 8. Que se passe-t-il lorsqu'une target passe à l'état DOWN ?

Prometheus n'arrive plus à récupérer ses métriques. La métrique `up` de cette target passe à `0` et les nouvelles valeurs ne sont plus collectées. Les anciennes données restent disponibles dans Prometheus.

## 9. Pourquoi est-il important de surveiller les ressources CPU, RAM et disque ?

Cette surveillance permet de détecter une saturation, d'anticiper une panne et de comprendre la cause d'un ralentissement. Elle aide aussi à adapter les ressources aux besoins du système.

## 10. Expliquer la différence entre les états UP et DOWN.

L'état `UP` signifie que Prometheus arrive à contacter la target et à récupérer ses métriques. L'état `DOWN` signifie que la collecte échoue à cause, par exemple, d'un service arrêté, d'une mauvaise adresse ou d'un problème réseau.

## 11. Pourquoi utilise-t-on la fonction `rate()` pour calculer l'utilisation CPU ?

La métrique `node_cpu_seconds_total` est un compteur cumulatif. La fonction `rate()` calcule sa vitesse d'évolution moyenne par seconde sur une période donnée. Cela permet de transformer le temps CPU cumulé en taux d'utilisation.

## 12. Pourquoi exclut-on généralement l'interface `lo` ?

L'interface `lo` est l'interface de boucle locale. Elle transporte uniquement les communications internes à la machine. On l'exclut pour ne pas mélanger ce trafic interne avec le trafic réseau réel entrant et sortant.
