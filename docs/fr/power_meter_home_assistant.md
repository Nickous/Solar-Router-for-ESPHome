# Compteur de puissance pour Home Assistant

Ce compteur de puissance est conçu pour obtenir la consommation électrique directement à partir d'un capteur Home Assistant.

Pour utiliser ce package, ajoutez les lignes suivantes à votre fichier de configuration :


```yaml linenums="1"
packages:
  power_meter:
    url: https://github.com/XavierBerger/Solar-Router-for-ESPHome/
    file: solar_router/power_meter_home_assistant.yaml
```

Ce package doit connaître le capteur à utiliser pour obtenir la consommation d'énergie. Il est attendu que ce capteur soit en Watts (W), qu'il soit positif (>0) lorsque l'électricité est consommée depuis le réseau et négatif (<0) lorsque l'électricité est envoyée au réseau. Ce capteur doit être défini par `main_power_sensor` dans la section `substitutions` de votre configuration, comme dans l'exemple ci-dessous :


```yaml linenums="1"
substitutions:
  # Power meter source -----------------------------------------------------------
  # Sensor in home assistant gathering the power consumption
  main_power_sensor: sensor.main_power
```

!!! warning "Disponibilité des données et fréquence de rafraîchissement"
    Ce compteur électrique s'appuie sur Home Assistant pour recueillir la valeur de l'énergie échangée avec le réseau. Il dépend également de la fréquence de mise à jour des capteurs. Si un capteur est mis à jour trop lentement, la régulation peut ne pas fonctionner comme prévu.

    Contrairement aux compteurs électriques de Home Assistant, les compteurs électriques natifs sont autonomes et peuvent continuer à réguler même si Home Assistant est hors ligne. Certains compteurs électriques peuvent avoir un accès direct aux mesures et peuvent même être indépendants du réseau.

