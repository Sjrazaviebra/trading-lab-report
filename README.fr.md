# 110 idées de trading, zéro survivant

> **Un compte rendu de méthode.** J'ai instruit 110 idées de trading sur deux ans de données d'or,
> avec une règle : la spécification **et le critère de rejet** sont écrits et horodatés dans `git`
> **avant** la première mesure.
>
> **Aucune n'a démontré d'avantage.** Ce qui reste, ce ne sont pas des stratégies — ce sont
> **21 règles de décision mesurées**, et **22 erreurs de ma part que le protocole a rattrapées**.

<sub>[English](README.md) &nbsp;·&nbsp; **Français**</sub>

## 🔎 [**Ouvrir le rapport interactif →**](https://sjrazaviebra.github.io/trading-lab-report/fr.html)

*Neuf onglets. **Le registre des 110 idées se déplie ligne par ligne** : ce que chacune
faisait, sa famille, son origine, et le motif qui l'a close. Recherche, filtres, tri. Les 21 règles
avec leur mesure, la chronique du laboratoire. Thème clair et sombre. Rien à installer.*

<sub>Vous préférez un seul fichier texte ? → [**RAPPORT.md**](RAPPORT.md)</sub>

---

### Trois choses qu'on y trouve et qu'on ne lit pas ailleurs

**La correction de rentabilité que personne n'affiche**
`p* = (R + c) / ((n + 1) × R)` — votre objectif à dix fois le risque n'exige pas 9,1 % de réussite,
**il en exige 10,5 % une fois le spread payé**. Sur les échelles courtes, cette seule correction
décide du signe du résultat.

**L'indicateur de flux qui aurait dit de vendre pendant que l'or doublait**
Sur **22 mois** et **34,8 millions de contrats** à terme, avec le sens de l'agresseur donné par la
place de marché : **le prix monte de 111 %, le déséquilibre cumulé perd 628 629 contrats.**

**`iATR` de MetaTrader 5 n'est pas l'ATR de Wilder**
C'est une moyenne simple glissante des *true ranges*. **Écart médian 8,9 %, 90ᵉ centile 25 %.**
Si vous calculez des seuils avec, ils ne sont pas ceux que vous croyez.

---

### Ce que ce dépôt contient — et ce qu'il ne contient pas

| ✅ contient | ⛔ ne contient pas |
|---|---|
| le rapport complet, rédigé de zéro | aucune donnée de marché *(redistribution interdite par les fournisseurs et les places de marché)* |
| les 21 règles, chacune avec son chiffre | aucun code de stratégie, aucun réglage retenu |
| les limites, auto-déclarées | aucune donnée personnelle, aucun identifiant de compte |

### ⚠️ Avertissement
Ceci **n'est pas un conseil en investissement**, ni une recommandation, ni une offre. Les performances
passées, mesurées ou simulées, ne préjugent pas des performances futures. Le trading à effet de levier
comporte un **risque de perte totale du capital**.

### Licence
Le texte est publié sous **[CC BY 4.0](LICENSE)** — réutilisable avec attribution.

*J. Razavi — septembre 2026*
