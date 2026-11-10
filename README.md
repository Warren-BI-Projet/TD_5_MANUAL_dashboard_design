# TD 5 — Tableaux de bord logistiques

Trois tableaux de bord présentent le même réseau de 20 villes françaises et trois entrepôts existants, avec des décisions différentes :

- [CO2](docs/co2.html) : liaisons à prioriser pour réduire les émissions ;
- [Coûts](docs/cost.html) : transport ou stockage selon l'entrepôt ;
- [Réseau](docs/network.html) : comparaison de l'ouverture de Bordeaux ou Marseille, de la fermeture de Lille et de la situation actuelle.

Les données de référence sont dans [data/cities.csv](data/cities.csv), les calculs dans [scripts/compute_kpis.py](scripts/compute_kpis.py), et les réponses aux sept questions dans [REFLECTIONS.md](REFLECTIONS.md). Le site statique démarre sur [docs/index.html](docs/index.html).

## Recalcul et consultation locale

Avec Python 3.12 ou plus récent :

```sh
python scripts/compute_kpis.py
python -m http.server 8000 --directory docs
```

Ouvrir ensuite `http://localhost:8000/`. Le workflow [compute.yml](.github/workflows/compute.yml) permet aussi de recalculer et committer les trois JSON depuis GitHub Actions, sur déclenchement manuel.

## Périmètre des chiffres

La demande annuelle est **estimée** à 50 tonnes pour 1 000 habitants. Les populations municipales sont approximatives : vérifier les valeurs courantes auprès de l'INSEE pour un usage professionnel. Les distances sont des distances orthodromiques entre centres de ville, pas des itinéraires routiers. Le facteur de 0,10 kg CO2e/tonne-km est illustratif et doit être confronté à la Base Empreinte de l'ADEME. Les coûts de 0,12 €/tonne-km et 40 €/tonne/an ne sont pas issus de tarifs observés.

Le contour simplifié de la France provient de [gregoiredavid/france-geojson](https://github.com/gregoiredavid/france-geojson), sous licence ouverte Etalab. L'analyse des scénarios ne tient pas compte des investissements, des baux, ni d'autres critères de service.
