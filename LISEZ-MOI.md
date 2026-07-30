# Xeler Devis — guide de mise en ligne et d'installation

## 1. Mettre l'application en ligne (une seule fois, 5 minutes, aucune compétence technique)

Pour que l'application soit installable sur téléphone Android, tablette et PC Windows 11, elle doit d'abord être hébergée en ligne (adresse internet sécurisée). Le plus simple, gratuit et sans code :

1. Aller sur **https://app.netlify.com/drop**
2. Glisser-déposer le dossier complet `xeler-devis-app` (celui qui contient `index.html`) dans la zone indiquée
3. Netlify donne une adresse du type `https://xeler-devis.netlify.app`
4. Cette adresse est celle à partager avec vos collaborateurs

Vous pouvez renommer cette adresse dans les réglages du site Netlify (bouton "Site settings" → "Change site name").

*Alternative : si vous préférez héberger sur le futur nom de domaine de la société, il suffira de déposer les mêmes fichiers sur l'hébergement du site web quand il sera prêt — l'application est conçue pour être reprise telle quelle.*

## 2. Installer l'application

### Sur Android / tablette
1. Ouvrir Chrome et se rendre sur l'adresse Netlify
2. Un bandeau "Ajouter à l'écran d'accueil" apparaît (ou menu ⋮ → "Installer l'application")
3. L'icône Xeler apparaît comme une application normale, hors ligne partiellement disponible

### Sur PC Windows 11 (y compris PC tactile 13 pouces)
1. Ouvrir Microsoft Edge ou Chrome et se rendre sur l'adresse Netlify
2. Cliquer sur l'icône d'installation dans la barre d'adresse (ou menu ⋮ → "Installer Xeler Devis")
3. L'application s'ouvre dans sa propre fenêtre, épinglable à la barre des tâches et au menu Démarrer

## 3. Premiers réglages (une fois installée)

Aller dans **Administration** :
- **Robots** : les 13 robots (7 Gausium, 4 Keenon, 2 Robotnik) sont maintenant préremplis avec les vraies photos et les prix HT de vente extraits de tes brochures — voir la note importante ci-dessous sur ces prix
- **Consommables** : ajuster la liste et les prix
- **Financement** : réglage du taux de mensualité Grenke (2,1 % par défaut), de la durée (60 mois) et du texte de mention légale — la mensualité est recalculée automatiquement à partir du prix HT de chaque robot, pas besoin de la saisir
- **Entreprise** : vérifier les coordonnées Xeler (déjà pré-remplies)
- **Envoi email** : renseigner votre adresse Exchange et le message type
- **Sauvegarde** : exporter le catalogue une fois vérifié, pour le partager à vos collaborateurs (voir point 4)

## 4bis. Photos et prix des robots — d'où ils viennent

Les photos ont été extraites directement des deux brochures PDF que tu as fournies (`Xeler_Gausium_Brochure_FINALE_nettoyage.pdf` et `..._surveillance_port.pdf`) — ce sont donc les visuels déjà validés, pas de nouvelles images.

**Important à vérifier avant utilisation client :** tes brochures n'affichaient qu'un tarif de location mensuelle ("Location dès X €HT/mois"), jamais le prix d'achat HT. Comme tu m'as donné la règle "mensualité = 2,1 % du prix sur 60 mois", j'ai fait le calcul à l'envers (prix = mensualité ÷ 0,021) pour retrouver un prix d'achat HT cohérent avec chaque mensualité déjà publiée :

| Robot | Mensualité brochure | Prix HT reconstitué |
|---|---|---|
| Tous les Gausium | 399 €/mois | 19 000 € |
| Keenon T8 | 399 €/mois | 19 000 € |
| Keenon T9 | 459 €/mois | 21 857 € |
| Keenon S100 | 389 €/mois | 18 524 € |
| Keenon S300 | 449 €/mois | 21 381 € |
| Robotnik RBwatcher | 690 €/mois | 32 857 € |

Ces montants sont mathématiquement cohérents avec tes propres tarifs affichés, mais je n'ai pas la facture d'origine — à confirmer/ajuster dans Administration si le prix d'achat réel diffère. Le RB-SUMMIT n'a pas de fiche ni de prix dans la brochure fournie (seul le RBwatcher, qui l'intègre, est commercialisé) — je l'ai laissé sans prix ni photo.

## 4. Important — partage des données entre collaborateurs

Chaque appareil stocke ses données (prix, robots) localement, en toute confidentialité. Il n'y a pas encore de synchronisation automatique entre les appareils.

**Après chaque mise à jour de prix ou de catalogue :**
1. Aller dans Administration → Sauvegarde → "Exporter catalogue & prix"
2. Envoyer le fichier `.json` obtenu à vos collaborateurs (email, Teams, clé USB...)
3. Chaque collaborateur l'importe depuis Administration → Sauvegarde → "Importer un fichier"

Cette étape manuelle sera supprimée lors du passage à la version en ligne connectée au futur site web (voir point 5).

## 5. Envoi des devis par email

Un navigateur ne peut pas se connecter directement à un serveur Exchange pour envoyer un email avec pièce jointe de façon totalement automatique, pour des raisons de sécurité. Le fonctionnement actuel :

1. Clic sur "Envoyer par email" dans l'aperçu du devis
2. Le PDF se télécharge automatiquement
3. Votre messagerie (Outlook) s'ouvre avec le destinataire, l'objet et le message déjà remplis
4. Il ne reste qu'à glisser le PDF téléchargé en pièce jointe et à cliquer sur Envoyer
5. L'accusé de réception peut être activé manuellement dans la fenêtre Outlook (option "Options" → "Demander un accusé de réception")

Une automatisation complète (envoi + pièce jointe + accusé sans intervention manuelle) est possible mais nécessite un petit serveur relais connecté à votre compte Exchange — c'est une évolution naturelle à prévoir quand l'application sera reliée au site web.

## 6. Évolution vers le configurateur en ligne du futur site

Le code de cette application est structuré pour être repris tel quel : le catalogue, le moteur de calcul de devis et la génération du document sont indépendants de l'interface. Ils pourront être branchés à une base de données partagée en ligne, ce qui permettra en plus :
- Un catalogue et des prix synchronisés automatiquement pour tous
- Un configurateur accessible directement par les clients depuis le site
- Un envoi d'email réellement automatique avec accusé de réception

## 7. Fiches techniques constructeur et catalogue

Dans **Catalogue**, cliquer sur un robot ouvre maintenant sa fiche technique officielle (le PDF constructeur, affiché directement dans l'application) avec un bouton "Retour au catalogue" et un bouton "Chiffrer ce robot" pour basculer directement vers le configurateur.

Au moment de télécharger ou d'envoyer un devis, la ou les fiches techniques des robots présents dans le devis sont **automatiquement fusionnées** à la suite du devis dans le même PDF final — un seul fichier à transmettre au client.

**Robots avec fiche technique déjà attachée :** les 7 modèles Gausium (PHANTAS, MIRA, MARVEL, OMNIE, BEETLE, VACUUM 40, SCRUBBER 75), à partir des brochures officielles que tu as fournies.

**Robots sans fiche pour l'instant :** Keenon T8/T9/S100/S300 et Robotnik RBwatcher — envoie-moi leurs brochures officielles (comme pour les Gausium) et je les intégrerai de la même façon. En attendant, leur fiche dans le catalogue affiche les caractéristiques déjà connues en remplacement du PDF.

**Important — cette fonctionnalité a besoin d'être hébergée en ligne pour fonctionner** (comme indiqué au point 1) : la fusion automatique des PDF utilise une requête technique qui ne fonctionne pas si tu ouvres simplement le fichier `index.html` depuis ton PC sans passer par une adresse web. Une fois déployée sur Netlify ou GitHub Pages, elle fonctionne normalement.

