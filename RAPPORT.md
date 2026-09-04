# 110 idées de trading, zéro survivant

### Ce qu'on apprend quand on s'oblige à écrire le critère de rejet avant de mesurer
*Deux ans de données sur l'or, un protocole scellé dans `git`, et 21 règles qui restent.*

---

> **Résumé en cinq lignes.** J'ai instruit 110 idées de trading sur deux ans de données, avec un
> protocole simple : la spécification **et le critère de rejet** sont écrits et horodatés dans `git`
> **avant** la première mesure. Aucune n'a démontré d'avantage. Ce que ce travail a produit n'est pas
> une stratégie — ce sont **21 règles de décision mesurées**, dont plusieurs contredisent ce qu'on lit
> partout, et **22 erreurs de ma part que le protocole a rattrapées avant qu'elles ne coûtent quelque
> chose.**

---

## Pourquoi lire ceci si vous ne tradez pas l'or

Ce rapport n'est pas un carnet de stratégies. C'est un **compte rendu de méthode** : ce qui se passe
quand on applique à ses propres idées la discipline qu'on exige des autres.

La plupart des tests de stratégie échouent d'une façon particulière : **ils ne peuvent pas échouer.**
Le critère est choisi après avoir vu les chiffres, l'étalon est zéro plutôt qu'une alternative
réelle, les frais arrivent en dernier, et le nombre d'essais n'est jamais compté. Le résultat a
l'air d'un test. Ce n'en est pas un.

J'ai voulu savoir ce qui survit quand on retire ces échappatoires une par une. **La réponse est :
rien.** Et l'intérêt du rapport est dans le *comment* — les 21 règles ci-dessous sont chacune née
d'un moment où j'ai failli me tromper, avec le chiffre exact qui m'en a empêché.

⚠️ **Ceci n'est pas un conseil en investissement**, ni une offre, ni une invitation à reproduire quoi
que ce soit avec de l'argent réel. Ce sont des mesures sur des données historiques, avec les limites
énumérées en fin de document.

---

## 1. Le protocole, en une page

**Sceller avant de mesurer.** Pour chaque idée : un fichier écrit qui contient la spécification, le
critère qui la tuerait, les seuils, les contrôles obligatoires — puis un commit. **Le hash du commit
est la preuve que rien n'a été choisi après coup.** Les scripts de mesure relisent ce hash et
refusent de tourner s'il ne correspond pas.

**Deux fenêtres, et une réserve.** Apprentissage `2024-01-01 → 2025-06-30`. Vérification
`2025-07-01 → 2025-12-31`. Une troisième période gardée vierge comme réserve — **lue une seule fois,
puis déclarée brûlée.** Elle a rendu `−0,06`. Aucun nouveau test n'y est autorisé.

**Épuiser le gratuit d'abord.** Avant de dépenser une lecture de la fenêtre de vérification, on épuise
tout ce qui se décide hors simulation : comptages, recouvrements, accords entre modules, arithmétique
de coût. **La plupart des idées meurent là, pour zéro.**

**Des placebos qui détruisent exactement ce qui est revendiqué.** Pas « un » témoin aléatoire : le
témoin qui détruit *précisément* la propriété que l'idée prétend exploiter, en conservant tout le
reste. Une idée qui prétend lire la direction est confrontée à un tirage de direction, à durée et à
amplitude conservées — 16 à 200 tirages selon le cas.

**Un étalon qui existe.** Jamais zéro. Pour un suiveur de tendance sur un actif qui monte, l'étalon
est **acheter et garder**. Pour un signal de direction, c'est la **position constante**. Et l'étalon
doit avoir **la même exposition** : comparer une stratégie investie 10 % du temps à une stratégie
investie en permanence n'est pas une comparaison, c'est une pénalité de construction.

**Compter les essais.** Le seuil de significativité est corrigé du nombre de cellules réellement
parcourues, et ce nombre est figé **avant** de regarder. Une grille de décision est limitée à trois
valeurs. Un balayage non spécifié a été chiffré une fois à `4×10²¹` combinaisons possibles : à ce
compte, **aucune mesure ne pouvait franchir 10 σ** — l'idée a été gelée avant le premier chiffre.

**`N_eff`, pas `N`.** Ce qui compte n'est pas le nombre de lignes mais le nombre d'observations
**effectivement indépendantes**. Un jeu de 12 000 lignes en valait **707**. Un autre : `8 818` au lieu
de `30 643` — assez pour faire passer un test de `9,99` (succès) à `8,20` (rejet).

**Un plancher de 30.** Sous trente observations, aucune statistique n'est publiée. Elle est remplacée
par un tiret.

> ### Le test qui dit si un protocole est réel
> **Est-ce qu'il vous a déjà empêché de publier quelque chose que vous vouliez publier ?**
> Celui-ci l'a fait **deux fois dans la même journée**, sur deux idées qu'une réécriture de seuil
> aurait sauvées — dont une qui échouait **à cinq centièmes** du sien — voir la section 5.

---

## 2. Les 21 règles, avec le chiffre qui les établit

Chacune est née d'une mesure, pas d'une lecture. Le chiffre entre parenthèses est celui qui l'a fixée.

### Sur l'étalon — « comparé à quoi ? »

**1. Pour un suiveur de tendance sur un actif qui monte, l'étalon est acheter-et-garder, jamais zéro.**
*Acheter et garder rendait **+1 767 $** là où la stratégie rendait **+984 $** — soit **80 % de plus**,
sans aucune règle.* Toute stratégie qui « gagne » sur un actif en tendance doit d'abord prouver
qu'elle bat le fait de ne rien faire.

**2. Un critère fondé sur le signe s'ancre sur la position constante, pas sur 50 %.**
*Écart apparié `z = −2,16` : le « toujours long » battait le critère testé.* Sur un actif qui dérive,
50 % n'est pas le hasard — le hasard, c'est la dérive.

**3. Un filtre ne vaut quelque chose que si le groupe qu'il BLOQUE est négatif — pas seulement « moins
bon ».** *Un filtre qui triait deux fois mieux détruisait quand même 30 % du résultat, parce que les
trades bloqués valaient encore **+259 $**.* Trier n'est pas filtrer.

**4. L'étalon doit être apparié sur l'EXPOSITION.** Comparer 10 % de temps investi à 100 % est une
pénalité de construction, pas une comparaison.

### Sur ce qui détruit — les couches ajoutées

**5. Toute couche qui BORNE une position ampute un suiveur de tendance, quel que soit le sens du
critère.** *Couper les **24 %** de positions qui dépassaient 12 fois la volatilité quotidienne retirait
**64 % du résultat net** (de 526 $ à 188 $).* Le gain vit dans une queue de positions très longues :
tout ce qui la coupe coupe le gain.

**6. Un critère de structure n'échappe à la règle 5 que s'il est RARE.**
*Une sortie « quand le sens rapide s'inverse » se déclenchait sur **90 % des positions** : c'est un
plafonnement sous un autre nom. Chiffré : **+1 125 $ sauvés** sur les petites perdantes contre
**−1 601 $ perdus** sur les grosses gagnantes — **1,42 $ perdu par dollar sauvé**.*

**7. Une couche qui ne place AUCUN ordre peut détruire autant qu'un module perdant.**
*Une règle de sortie a coûté **−1 022 $** ; un module qui plaçait 162 trades perdants en coûtait
**−1 090 $**. Presque à égalité — et l'un des deux ne trade pas.*

**8. Un coupe-circuit est un instrument de CHUTE, pas de rendement.**
*Il abaisse la chute sur **7 instruments sur 8**. Sur le rendement, sans avantage il est neutre ; avec
un avantage il en détruit une part.*

**9. Pousser un garde-fou jusqu'à changer la nature de l'objet invalide la mesure.**
*À **35 %** de journées coupées, ce n'est plus un coupe-circuit : c'est un stop journalier serré. La
passe entière a été invalidée.*

**10. Aucune gestion du risque ne remplace un avantage.**
*Un témoin qui entre au hasard, avec le coupe-circuit et tous les plafonds actifs, a vidé **1 900 $
d'un compte de 2 000 $**.* C'est la règle fondatrice : le risque protège un avantage, il n'en crée pas.

### Sur les témoins — « comment sait-on que ce n'est pas du hasard ? »

**11. Le témoin doit détruire EXACTEMENT ce que l'idée revendique.**
*Un témoin mal ciblé rendait `21,9 ± 6,3` là où l'observé valait `18` — l'idée semblait passer. Le
témoin correct, qui détruisait la bonne propriété, l'a tuée.*

**12. Toute statistique bâtie sur un MAXIMUM est surtout de la diffusion.**
*Un tirage purement aléatoire capturait déjà **86 %** de l'excursion favorable maximale observée.*
Excursion maximale, plus haut atteint, meilleur gain latent : ce sont des maximums, et un maximum
grandit tout seul avec le temps.

**13. Toute statistique de déplacement SIGNÉ sur un actif qui dérive mesure la dérive.**
*Une fois la série détrendée, la statistique tombait de **−88 %** et la proportion de positions
longues passait de **70 % à 53 %** — pile ou face. L'actif avait monté de **+59,9 %** sur la période.*

**14. Quand un critère pré-inscrit semble échouer, vérifier le témoin AVANT d'y toucher.**
*Le bon témoin faisait échouer les **12 cellules** de toute façon.* Changer le critère parce qu'il
échoue, c'est arrêter de tester.

**15. 84 % des grilles ALÉATOIRES passaient l'un de mes critères.**
*Mesuré sur **20 000 tirages**.* Un critère qu'une grille au hasard franchit quatre fois sur cinq ne
filtre rien du tout.

### Sur les instruments de mesure — « l'outil ment-il ? »

**16. Sur un résultat net, un estimateur de RANG mesure d'abord le régime de frais du courtier.**
*L'autocorrélation du **péage seul** valait **+0,86**.* On croit mesurer la stratégie ; on mesure le
spread.

**17. Face à un coût de queue, la médiane est l'instrument qui le cache.**
*La médiane du spread par créneau horaire était plate entre **20 et 31** points, ce qui suggérait
qu'aucune heure n'était chère. Le **90ᵉ centile** à 23 h valait **90** et le **99ᵉ**, **118**.* La
médiane a répondu « aucun créneau cher sur 92 » à une question dont la réponse était dans la queue.

**18. Un rapport dont le dénominateur n'est pas significativement différent de zéro n'est pas une
mesure.** *Un rapport de **7,20** paraissait franchir un seuil de 3 — jusqu'à ce qu'on regarde son
dénominateur : `+0,0128 ± 0,0129`, soit `t = 0,99`.* C'était une division par du bruit.

**19. Mesurer une redondance sur des POSITIONS au lieu d'AVIS gonfle l'accord.**
*`0,70` contre `0,60` — assez pour franchir ou non le seuil de redondance.*

**20. Toute question portant sur l'ÉTAT d'une position se règle en simulation complète, jamais par
reconstruction hors ligne.** *Erreur mesurée : **un facteur 100**.* Trois fuites successives, toutes
favorables à l'idée testée : tronquer une perte en gardant la position, payer un écart de nuit à une
position à plat, et laisser dériver l'objet mesuré.

**21. Un résultat qui contredit un fait déjà mesuré est un signal d'INSTRUMENT, jamais une découverte.**
*Appliqué trois fois en une journée ; les trois fois, le défaut était dans mon outil.*

---

## 3. La règle la plus dure, et elle porte sur le protocole lui-même

> ### Une seule convention non écrite suffit à inverser un verdict déjà rendu.
> **Cinq verdicts sur cinq ont été retournés en un seul tour de contre-expertise**, chacun par une
> seule convention que personne n'avait pensé à écrire : la phase d'un découpage temporel, la
> définition exacte d'un seuil, la taille d'une brique de comptage.

C'est la découverte la plus inconfortable de ce travail. Un protocole peut être rigoureux **et faux**,
parce que la rigueur porte sur ce qui est écrit et que le décisif est souvent ce qui ne l'est pas.

**La parade adoptée** : un relecteur indépendant qui **recalcule** au lieu de relire, et qui franchit
la frontière de langage — si la mesure est en Python, il la refait à partir du code de production, et
inversement. Une réimplémentation indépendante a ainsi reproduit une série de signaux **161 sur 161,
au bit près**, ce qui a validé le harnais ; ailleurs, la même méthode a révélé qu'un chiffre de
référence utilisé pendant des semaines (`162`) contredisait la pièce gelée qui en contenait `161`.

---

## 4. Sept idées, et pourquoi elles sont mortes

Sept parmi cent dix. Choisies parce que chacune montre un piège différent.

### L'or déguisé en signal
Une règle multi-échelles semblait porter une vraie information directionnelle : son témoin ne
l'égalait **jamais** sur 200 tirages. Elle passait.

**Elle ne passait que parce que le témoin effaçait la dérive.** L'actif avait monté de **59,9 %** sur
la période, et la règle partait à l'achat **70 % du temps**. Sur la série détrendée, l'avantage
tombait de **−88 %** et la proportion de positions longues descendait à **53 %** — pile ou face.
*Le couperet mesurait le marché, pas la règle.*

### La médiane qui cachait la note
Une idée proposait de retarder les ordres qui tombent aux minutes où le spread est cher. Premier
calcul : **aucun créneau cher sur 92** — l'idée semblait sans objet.

Mais ce résultat contredisait un fait déjà mesuré : le spread de nuit est nettement plus élevé. J'ai
donc vérifié mon instrument avant de publier. **La médiane par créneau était plate ; la queue ne
l'était pas** — 90ᵉ centile à **90** points et 99ᵉ à **118** à 23 h, contre **53** et **72** en pleine
séance. *La bonne réponse était dans la queue, et je regardais le milieu.*

### Le seuil qui exigeait l'impossible
Un déclencheur de compression de volatilité tire **59,4 %** de ses signaux la nuit, contre **42,4 %**
attendus — un biais de **+40 %** causé par le simple fait qu'un creux nocturne *ressemble* à une
compression. Le correctif existe et **change 41 à 47 % des décisions**.

Mon critère pré-inscrit exigeait une concentration nocturne de « **au moins 2 fois** l'attente ».
**Or la nuit représente déjà 42 % des barres : « 2 fois » aurait exigé 85 % des signaux la nuit** —
un quasi-maximum. Le critère était arithmétiquement presque impossible à satisfaire.

**Je l'ai appliqué quand même, et l'idée est classée.** Réécrire un seuil après avoir vu le résultat
est exactement ce qui rend un test inutile — y compris quand le résultat vous plairait.

### La cassure d'ouverture qui meurt sur les frais, pas sur le signal
Une cassure de la première bougie de séance, stop de l'autre côté, objectif dix fois le risque.
Pour être rentable **sans aucun frais**, il faut réussir `1/11 = 9,09 %` du temps.

Mesuré sur **1 034 cassures** : **9,59 %** sur la première période, **9,16 %** sur la seconde.
**Elle franchit la barre — deux fois.**

Les frais la déplacent à **10,5 %**. **Elle tombe pile dans l'intervalle, deux fois.**

> C'est la formule la plus utile de tout ce travail, et elle vaut pour n'importe qui :
> ### `p* = (R + c) / ((n + 1) × R)`
> où `R` est le risque, `c` le coût aller-retour, `n` l'objectif en multiples du risque.
> **Un objectif à 10R n'exige pas 9,1 % de réussite. Il en exige 10,5 % une fois le spread compté.**
> Aucun outil grand public n'affiche cette correction.

### L'indicateur de flux qui aurait dit de vendre pendant que l'or doublait
Le déséquilibre acheteur-vendeur cumulé — l'indicateur central de toute une école d'analyse — a pu
être calculé sur des données réelles de contrats à terme : **22 mois, 34,8 millions de contrats**,
avec le sens de l'agresseur donné par la place de marché et non deviné.

**Le prix a monté de 111 %. Le cumul a perdu 628 629 contrats.**

La lecture usuelle (« cumul négatif ⇒ baissier ») aurait été fausse **vingt-deux mois d'affilée**. Ce
n'est pas une surprise théorique : la littérature prédit exactement cela — le flux brut est dominé par
sa part **prévisible**, celle que la liquidité absorbe et qui ne déplace pas le prix.

### La famille qu'on voit partout, mesurée pour la première fois
Blocs d'ordres, ruptures de structure, écarts de valeur : une famille très diffusée, que j'avais
classée en juillet **sur une revue de littérature** — donc mal.

Définitions figées d'avance, sans adjectif, puis mesure : **0 sur 6 cellules**, avantage contre la
position constante **négatif dans les six**, avec des `t` jusqu'à **−6,5**.

**Mais ce n'est pas le `t` qui tranche, c'est le comptage** : l'un des motifs apparaît **6 725 fois
sur 34 762 barres — un événement toutes les cinq bougies.** Ce n'est pas une détection, c'est une
description de l'action des prix ordinaire.

> **Un critère qui se déclenche partout n'est pas un critère.** Et on ne le répare pas en ajoutant des
> filtres : filtrer 6 725 événements jusqu'à en garder 50, c'est **choisir 50 événements après coup**.

### L'idée tuée par une division
Une proposition suggérait d'exécuter pendant la minute où l'impact de marché est mesuré plus faible :
`0,0022 %` par **million de dollars** échangés.

La taille réellement tradée était **une once**, soit environ **3 000 $**. **L'effet recherché est
mille fois plus petit que les frais ordinaires.** Il n'y avait rien à mesurer : le poids de l'idée
était écrit dans les **unités** de sa propre source.

*Cinq idées de la même famille sont mortes ainsi, pour le prix d'une division.*

---

## 5. Mes erreurs — vingt-deux, et comment chacune a été attrapée

Cette section est la raison d'être du rapport. **Un protocole ne se juge pas sur ce qu'il valide,
mais sur ce qu'il a empêché son auteur de croire.**

### Les cinq qui ont failli passer

**Un facteur 4 qui en valait 44.** J'avais écrit qu'il manquait « environ 4 fois » plus d'historique
pour conclure. En relisant mon propre journal du matin, le vrai chiffre était **44**. Onze fois pire,
et la conclusion opposée.

**Le meilleur tirage pris pour la moyenne.** J'avais publié un résultat comme s'il était la performance
typique. C'était **le meilleur de seize tirages**. Ma propre consigne disait de lire les deux — je ne
l'avais pas suivie.

**Un positif qui n'existait qu'en unités de frais.** Une stratégie « gagnait » sur trois instruments
quand on comptait en multiples du spread. Convertie en monnaie, le troisième valait **+45 $** sur deux
ans — économiquement nul. **Elle ne gagnait que sur deux.**

**Un résultat trop propre.** Une identité comptable rendait exactement **+0,00 $** sur 49 positions.
C'était trop parfait pour être vrai : la vérification a montré que **121 sorties sur 123 ne portaient
aucune étiquette de module** — mon appariement associait des sorties aux mauvaises entrées. *Le
« résultat » était un artefact de mon propre code.*

**Une idée déclarée autorisée alors que je l'avais réfutée.** J'avais écrit un matin qu'une idée était
prête à être construite, « la seule à passer tous ses contrôles ». En allant chercher sa spécification
pour commencer à coder, j'ai trouvé dans **mon propre journal** la réfutation que j'avais publiée
**trois jours plus tôt**. Elle avait passé quatre contrôles — mais tous les quatre vérifiaient qu'elle
était *différente* des autres, **aucun ne vérifiait qu'elle prédisait quoi que ce soit**.

### Les erreurs d'outil

- **`iATR`, la fonction d'ATR de MetaTrader 5, n'est pas l'ATR de Wilder.** C'est une moyenne simple
  glissante des *true ranges*. **Écart médian 8,9 %, 90ᵉ centile 25 %.** J'ai construit des seuils
  pendant des semaines en croyant faire du Wilder. *Ce point à lui seul concerne tout développeur
  MetaTrader.*
- **Un plancher de perte pris pour un pourcentage.** Une règle de société de financement est un
  **montant fixe** sous le plus haut solde réalisé, jamais réinitialisé — pas un pourcentage de
  l'équité flottante. Corrigée, la marge de survie était multipliée par **huit**.
- **Une erreur d'algèbre sur un seuil.** Un encodage `f ≥ 0` que je lisais comme « indice ≥ 25 »
  codait en réalité « ≥ 50 ». Le bit s'activait sur **3 %** des barres au lieu de **43 %**. Le verdict
  s'est inversé.
- **Un témoin qui détruisait la mauvaise propriété.** Mon témoin cassait l'autocorrélation de la série
  (`0,73 → 0,13`) alors que la propriété testée, elle, restait intacte. Il ne prouvait rien.

### Les deux refus qui coûtent

Deux fois dans la même journée, **réécrire un seuil aurait sauvé une idée**. Deux fois, refusé.

- Un critère exigeait « 2 fois l'attente » là où la grandeur ne pouvait presque pas l'atteindre. Le
  biais réel était pourtant confirmé, à **+40 %**. **Idée classée.**
- Un critère exigeait un rapport de 3 sur les deux moitiés de l'échantillon. Mesuré : **2,95** — à
  cinq centièmes. Le mécanisme était par ailleurs confirmé, avec des `t` allant jusqu'à **+56**.
  **Idée classée.**

> **La cohérence de la règle EST la règle.** J'avais refusé le matin de déplacer un seuil quand cela
> jouait *contre* une idée. Je ne pouvais pas l'accepter l'après-midi parce que cela jouait *pour*.

### Onze verdicts retournés

Onze fois, un verdict déjà rendu a été inversé — parfois deux fois de suite pour la même idée : rendue
close, rouverte par une erreur d'algèbre, refermée sur un motif neuf après lecture d'une pièce jointe.
**C'est le fonctionnement normal du dispositif, pas son échec.**

---

## 6. Ce qui reste, et qui vaut indépendamment de tout ceci

### La correction de rentabilité — utile à n'importe qui
`p* = (R + c) / ((n + 1) × R)`. **Votre objectif à 10 fois le risque n'exige pas 9,1 % de réussite ;
il en exige 10,5 % une fois le spread payé.** Sur les échelles courtes, cette correction décide seule
du signe du résultat.

### Le dimensionnement — la chute est un montant, pas un pourcentage
Une stratégie donnée produit une chute d'un **nombre fixe de monnaie par unité de taille minimale**.
Ce qui varie, c'est le compte. Le même module représentait **21 % d'un petit compte et 4 % d'un compte
cinq fois plus grand.**

Deux conséquences que personne n'affiche :
1. **La contrainte totale et la contrainte journalière ne mordent pas sur les mêmes stratégies.** La
   journalière mord sur les **rapides** ; la totale sur les **lentes** — chute quotidienne médiane
   faible, mais accumulée sur des semaines. *Il faut calculer les deux et prendre le minimum.*
2. **Un calculateur de taille doit pouvoir répondre « non ».** À la taille minimale imposée par le
   courtier, avec une marge de sécurité raisonnable, certaines stratégies exigent un compte plusieurs
   fois plus gros que celui de l'utilisateur. **Un calculateur qui rend toujours un nombre ment.**

### Trois faits techniques, hors stratégie
- **`iATR` n'est pas Wilder** (8,9 % d'écart médian, 25 % au 90ᵉ centile).
- **Le carnet d'ordres n'est jamais archivé** : *zéro* retour non vide sur **139 440** appels en
  simulation. Ce n'est pas une question d'abonnement — la donnée n'existe nulle part *a posteriori*.
- **51,9 % des événements du carnet ne changent aucun prix** : ils sont donc **invisibles** dans un
  flux de ticks. Toute étude de carnet reconstruite depuis des ticks en ignore la moitié.

### Le coût réel d'un aller-retour
Sur l'instrument étudié, le spread médian vaut **23 points**, mais son 99ᵉ centile atteint **90**, et
son maximum **259**. Le coût de portage d'une nuit vaut **58 points** — soit **plus du double du
spread médian**, et il est **triplé un jour par semaine** (le mercredi pour les métaux et les devises,
le vendredi pour les indices). *Une stratégie qui garde ses positions la nuit paie son portage
plusieurs fois le prix de son spread, et presque personne ne l'affiche.*

---

## 7. Ce que ce rapport ne dit pas

Cette section est aussi importante que les précédentes. Les limites qui suivent sont **auto-déclarées**
et n'ont été demandées par personne.

**Les chiffres de référence ne sont pas adossés à des pièces hachées.** Les rapports de simulation
détaillés, trade par trade, sont **introuvables sur disque pour 41 des 42 dossiers concernés**. Les
performances phares de ce travail vivent dans des tableaux de synthèse, **pas dans des artefacts
vérifiables**. ⚠️ *Un lecteur qui demanderait la pièce ne l'obtiendrait pas.* C'est la limite la plus
sérieuse de l'ensemble, et elle porte précisément sur les nombres qu'on aurait envie de citer.

**Un seul instrument principal, une seule période.** L'essentiel porte sur **l'or au comptant (XAU/USD)**, en barres de
quinze minutes, sur **2024-2025** — une période de **forte tendance** (+59,9 % sur la première
moitié). Une règle mesurée sur une tendance ne dit rien d'un marché sans direction, et cela a été
vérifié : le réglage optimal d'un frein s'**inverse** selon le régime.

**Une fenêtre de vérification lue onze fois.** Chaque lecture supplémentaire affaiblit la garantie
hors échantillon. La réserve vierge a été consommée en une seule lecture et déclarée brûlée.

**Granularité de barre.** Les reconstructions hors simulation travaillent à la barre, pas au tick.
C'est explicitement insuffisant pour tout ce qui touche à l'exécution : une mesure d'ordre à cours
limité y affichait un taux de service de **90 %**, ce qui n'est pas crédible et prouve que
l'instrument ne pouvait pas trancher.

**Plusieurs verdicts récents n'ont eu aucune contre-expertise.** Le relecteur adverse n'était pas
disponible sur les dernières séries : ces verdicts sont **révocables sur pièce**, et c'est écrit dans
chacun d'eux.

**Ce n'est pas une preuve d'impossibilité.** 110 idées testées, ce n'est pas « les marchés sont
efficients ». C'est : **ces 110 idées-là, mesurées ainsi, sur ces données-là, ne montrent pas
d'avantage.** Une idée absente de la liste n'est pas réfutée par ce travail.

---

## 8. Ce qui n'est pas publié, et pourquoi

Par souci de transparence sur la transparence même :

- **Les données de marché sont absentes.** Elles proviennent de fournisseurs dont les conditions
  d'utilisation interdisent la redistribution, et les données de contrats à terme relèvent d'une
  licence de place de marché. **Les empreintes cryptographiques des jeux gelés existent** et
  permettent de vérifier qu'un jeu n'a pas bougé — sans redistribuer les prix.
- **Le code de stratégie n'est pas publié.** La méthode se publie ; les réglages retenus, non.
- **Aucune donnée personnelle, aucun identifiant de compte, aucun chemin de machine** n'apparaît ici.
  Ce document a été **rédigé de zéro**, pas extrait d'archives internes, précisément pour cette raison.

---

## En un paragraphe

J'ai testé cent dix idées de trading en m'obligeant à écrire d'avance ce qui les tuerait. **Aucune n'a
survécu.** Ce n'est pas le résultat que j'espérais, mais c'est un résultat : il a coûté zéro euro de
capital risqué, il est daté et horodaté idée par idée, et il a produit vingt et une règles de décision
qui, elles, tiennent. La plus utile tient en une ligne — **votre objectif à dix fois le risque exige
10,5 % de réussite, pas 9,1 %** — et la plus dure aussi : **une seule convention non écrite suffit à
inverser un verdict déjà rendu.**

Si un seul point de ce rapport devait être retenu, ce serait celui-ci :

> **Un protocole qui n'a jamais rien tué ne prouve rien.**
> Celui-ci a tué cent dix idées, dont deux qu'une réécriture de seuil aurait sauvées — l'une à **cinq centièmes** près.

---

*Document publié à titre informatif. **Ceci n'est pas un conseil en investissement**, ni une
recommandation, ni une offre. Les performances passées, mesurées ou simulées, ne préjugent pas des
performances futures. Le trading à effet de levier comporte un risque de perte totale du capital.*

*J. Razavi — septembre 2026*
