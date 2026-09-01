# A.D.O

## Projet d'assistant vocal personnel Android


# 0. Objectif du projet


Créer un assistant vocal personnel Android

L'assistant devra être capable de :

- écouter une commande vocale ;
- comprendre une commande ;
- répondre vocalement ;
- contrôler la lecture musicale ;
- passer à la musique suivante ;
- revenir à la précédente ;
- lancer une playlist ou une musique lorsque l'app cible le permet ;
- ouvrir une application ;
- rechercher un contact ;
- appeler un contact ;
- détecter un appel entrant ;
- répondre à un appel ;
- refuser un appel ;
- préparer / envoyer un message avec permission ;
- fonctionner en arrière-plan ;
- être activé par un Mot Magique ;
- fonctionner hors ligne ;
- éventuellement utiliser une IA pour les commandes complexes.


---


# PHASE 01 — Créer le projet

## Objectif de la phase

Obtenir une application Android vide qui se compile et s'installe correctement.

---

## 01.01 — Installer / vérifier Android Studio

### À faire

- [ ] Vérifier qu'Android Studio est installé.
- [ ] Vérifier que le SDK Android est installé.
- [ ] Vérifier qu'un appareil Android ou un émulateur est disponible.
- [ ] Vérifier que Gradle fonctionne.

### Résultat attendu


Android Studio
      ↓
SDK disponible
      ↓
Appareil disponible
      ↓
Projet compilable


---

## 01.02 — Créer le projet

### À faire

- [ ] Créer un nouveau projet.
- [ ] Choisir Kotlin.
- [ ] Choisir Jetpack Compose.
- [ ] Choisir Material 3.
- [ ] Définir le nom de l'application.
- [ ] Définir le package.
- [ ] Choisir le SDK minimum adapté au projet.
- [ ] Créer le projet.

### Résultat attendu

Le projet apparaît correctement dans Android Studio.

---

## 01.03 — Compiler le projet

### À faire

- [ ] Synchroniser Gradle.
- [ ] Compiler.
- [ ] Corriger les éventuelles erreurs.

### Résultat attendu

La compilation se termine avec succès.


---

## 01.04 — Installer l'application

### À faire

- [ ] Installer sur le téléphone.
- [ ] Ouvrir l'application.

### Résultat attendu

Une application vide s'ouvre sur le téléphone.


---

# PHASE 02 — Créer l'interface minimale

## Objectif

Avoir un écran qui permet de voir ce que fait actuellement l'assistant.

---

## 02.01 — Créer l'écran principal

### À faire

- [ ] Créer `MainScreen`.
- [ ] Ajouter le titre.
- [ ] Ajouter un texte d'état.

### Résultat attendu

L'application affiche :

Assistant

État : En veille

---

## 02.02 — Ajouter un bouton microphone

### À faire

- [ ] Ajouter un bouton.
- [ ] Ajouter une icône microphone.
- [ ] Ajouter un texte.

### Résultat attendu

Un bouton :


🎙️ Écouter


est visible.

---

## 02.03 — Faire changer le texte

### À faire

Lorsque le bouton est pressé :


État : En écoute


- [ ] Ajouter l'état.
- [ ] Modifier l'état au clic.
- [ ] Afficher l'état.

### Résultat attendu

Appuyer sur le bouton change réellement l'interface.

---

# PHASE 03 — Créer le système d'état

## Objectif

Le reste de l'application doit pouvoir savoir ce que fait actuellement l'assistant.

---

## 03.01 — Créer `AssistantState`

Créer :


IDLE
LISTENING
PROCESSING
EXECUTING
SPEAKING
ERROR


### Résultat attendu

Tous les états de base existent dans le code.

---

## 03.02 — Créer `AssistantViewModel`

### À faire

- [ ] Créer le ViewModel.
- [ ] Ajouter un `StateFlow`.
- [ ] Stocker l'état actuel.

### Résultat attendu

L'interface peut observer l'état de l'assistant.

---

## 03.03 — Tester les changements

### À faire

Créer temporairement des boutons permettant de passer entre les états.

### Résultat attendu


IDLE
 ↓
LISTENING
 ↓
PROCESSING
 ↓
EXECUTING
 ↓
SPEAKING
 ↓
IDLE


fonctionne correctement.

---

# PHASE 04 — Autorisation microphone

## Objectif

Permettre à l'application d'utiliser le microphone.

---

## 04.01 — Ajouter la permission

### À faire

Ajouter :


android.permission.RECORD_AUDIO


### Résultat attendu

Android connaît la permission nécessaire.

---

## 04.02 — Vérifier la permission

### À faire

- [ ] Vérifier si elle est accordée.
- [ ] Afficher le résultat.

### Résultat attendu

L'application sait distinguer :


Microphone autorisé
Microphone refusé


---

## 04.03 — Demander la permission

### À faire

- [ ] Afficher une explication.
- [ ] Demander la permission.
- [ ] Gérer l'autorisation.
- [ ] Gérer le refus.

### Résultat attendu

Au premier lancement, Android demande l'accès au microphone.

---

## 04.04 — Tester le refus

### À faire

- [ ] Refuser la permission.
- [ ] Relancer l'application.
- [ ] Vérifier le comportement.

### Résultat attendu

L'application ne plante pas.

Elle indique simplement que le microphone n'est pas disponible.

---

# PHASE 05 — Speech-to-Text

## Objectif

Transformer la voix de l'utilisateur en texte.

---

## 05.01 — Vérifier la disponibilité

### À faire

- [ ] Vérifier que `SpeechRecognizer` est disponible.
- [ ] Prévoir le cas où il ne l'est pas.

### Résultat attendu

L'application sait si Android peut effectuer la reconnaissance vocale.

---

## 05.02 — Créer `SpeechRecognizerManager`

### À faire

Créer une classe responsable uniquement de :


Démarrer écoute
Arrêter écoute
Recevoir résultat
Recevoir erreur
Libérer ressources


### Résultat attendu

Le code vocal n'est pas mélangé avec l'interface.

---

## 05.03 — Démarrer l'écoute

### À faire

- [ ] Appuyer sur le bouton.
- [ ] Démarrer SpeechRecognizer.
- [ ] Passer à `LISTENING`.

### Résultat attendu

Le téléphone écoute réellement.

---

## 05.04 — Recevoir un résultat

Dire :

> Bonjour

### Résultat attendu

L'écran affiche :


Texte reconnu :
Bonjour


---

## 05.05 — Gérer aucun résultat

### Résultat attendu

Si rien n'est compris :


Aucune commande comprise.


---

## 05.06 — Gérer les erreurs

Tester :

- [ ] Microphone indisponible.
- [ ] Reconnaissance interrompue.
- [ ] Aucun résultat.
- [ ] Service indisponible.

### Résultat attendu

Aucun crash.

---

# PHASE 06 — Text-to-Speech

## Objectif

Faire parler l'assistant.

---

## 06.01 — Initialiser TTS

### À faire

Créer :


TextToSpeechManager


### Résultat attendu

Le moteur TTS démarre correctement.

---

## 06.02 — Sélectionner le français

### À faire

- [ ] Vérifier la langue française.
- [ ] Utiliser la voix française disponible.

### Résultat attendu

L'assistant parle en français.

---

## 06.03 — Créer `speak()`

### À faire

Créer :


speak("Bonjour")


### Résultat attendu

Le téléphone prononce :

> Bonjour

---

## 06.04 — Arrêter la voix

### À faire

Créer une fonction d'arrêt.

### Résultat attendu

L'assistant peut arrêter sa réponse vocale.

---

## 06.05 — Libérer TTS

### À faire

- [ ] Arrêter TTS.
- [ ] Libérer la ressource.

### Résultat attendu

Aucune fuite de ressource lorsque l'application est fermée.

---

# PHASE 07 — Première vraie conversation

## Objectif

Faire fonctionner :


Voix → texte → compréhension simple → réponse vocale


---

## 07.01 — Reconnaître "bonjour"

### Résultat attendu


Utilisateur : Bonjour
Assistant : Bonjour !


---

## 07.02 — Reconnaître "ça va"

### Résultat attendu


Utilisateur : Ça va ?
Assistant : Oui, tout va bien.


---

## 07.03 — Commande inconnue

### Résultat attendu


Utilisateur : blablabla
Assistant : Je n'ai pas compris.


---

# PHASE 08 — Système d'Intent

## Objectif

Transformer le texte en une commande structurée.

---

## 08.01 — Créer `Intent`

Créer :


UNKNOWN
PLAY
PAUSE
NEXT_MEDIA
PREVIOUS_MEDIA


### Résultat attendu

Chaque commande possède un identifiant clair.

---

## 08.02 — Ajouter les paramètres

Créer une structure permettant par exemple :


OPEN_APP("Discord")
CALL_CONTACT("Thomas")
SET_VOLUME(30)


### Résultat attendu

Une intention peut transporter des informations.

---

## 08.03 — Tester sans voix

Entrée :


"pause"


Sortie :


PAUSE


### Résultat attendu

Le système de commandes fonctionne même sans microphone.

---

# PHASE 09 — CommandParser

## Objectif

Créer le cerveau simple qui comprend les formulations connues.

---

## 09.01 — Parser PLAY

Reconnaître :


joue
lance la musique
reprends
mets la musique


### Résultat attendu

Toutes donnent :


PLAY


---

## 09.02 — Parser PAUSE

Reconnaître :


pause
mets en pause
arrête la musique


### Résultat attendu

Toutes donnent :


PAUSE


---

## 09.03 — Parser NEXT

Reconnaître :


suivante
passe à la suivante
musique suivante


### Résultat attendu

Toutes donnent :


NEXT_MEDIA


---

## 09.04 — Parser PREVIOUS

Reconnaître :


précédente
reviens à la précédente
musique précédente


### Résultat attendu

Toutes donnent :


PREVIOUS_MEDIA


---

## 09.05 — Commande inconnue

### Résultat attendu

Une phrase non reconnue donne :


UNKNOWN


---

# PHASE 10 — CommandExecutor

## Objectif

Séparer la compréhension de l'exécution.


Parser
 ↓
Intent
 ↓
Executor


---

## 10.01 — Créer `CommandExecutor`

### Résultat attendu

Une classe centrale reçoit les Intent.

---

## 10.02 — Créer `CommandResult`

Créer :


SUCCESS
FAILURE
NOT_FOUND
NOT_SUPPORTED
NEEDS_PERMISSION
NEEDS_CONFIRMATION


### Résultat attendu

Chaque action peut retourner un résultat compréhensible.

---

## 10.03 — Exécuter une commande fictive

Créer temporairement :


PLAY
 ↓
SUCCESS


### Résultat attendu

Le système complet fonctionne sans encore contrôler Android.

---

# PHASE 11 — Contrôle musical basique

## Objectif

Contrôler les médias Android sans dépendre directement de ton application musicale.

---

## 11.01 — Étudier MediaSession

### À faire

- [ ] Comprendre MediaSession.
- [ ] Comprendre MediaController.
- [ ] Comprendre les commandes de transport.

### Résultat attendu

Tu sais comment Android expose les commandes multimédia.

---

## 11.02 — Envoyer PLAY

### Résultat attendu

Une application musicale compatible commence la lecture.

---

## 11.03 — Envoyer PAUSE

### Résultat attendu

La musique se met en pause.

---

## 11.04 — Envoyer NEXT

### Résultat attendu

La piste suivante est sélectionnée.

---

## 11.05 — Envoyer PREVIOUS

### Résultat attendu

La piste précédente est sélectionnée.

---

## 11.06 — Connecter le parser

### Résultat attendu


"Lance la musique"
 ↓
PLAY
 ↓
MediaSession
 ↓
🎵 Lecture


---

## 11.07 — Tester avec ton application musicale

### Résultat attendu

Ton application musicale réagit aux commandes sans que l'assistant soit intégré dedans.

---

# PHASE 12 — Lancer une application

## Objectif

Dire :

> Ouvre Discord

et ouvrir Discord.

---

## 12.01 — Récupérer les applications

- [ ] Utiliser `PackageManager`.
- [ ] Récupérer les applications lançables.
- [ ] Récupérer leur nom.

### Résultat attendu

L'assistant possède une liste d'applications utilisables.

---

## 12.02 — Rechercher une application

Créer :


findApplication("Discord")


### Résultat attendu

La fonction retourne l'application correspondante.

---

## 12.03 — Gérer application inexistante

### Résultat attendu


"Je ne trouve pas cette application."


---

## 12.04 — Créer `AppLauncher`

### Résultat attendu

Une fonction permet d'ouvrir une application.

---

## 12.05 — Créer `OPEN_APP`

### Résultat attendu


"ouvre Discord"
 ↓
OPEN_APP("Discord")
 ↓
Discord


---

# PHASE 13 — Contrôle du volume

## 13.01 — Volume +

### Résultat attendu

> Monte le son

augmente le volume approprié.

---

## 13.02 — Volume -

### Résultat attendu

> Baisse le son

diminue le volume approprié.

---

## 13.03 — Volume précis

Comprendre :

> Mets le volume à 30 %

### Résultat attendu


SET_VOLUME(30)


---

## 13.04 — Valeurs invalides

Tester :


-10 %
150 %


### Résultat attendu

La valeur est rejetée ou limitée de manière contrôlée.

---

# PHASE 14 — Contacts

## 14.01 — Permission contacts

### Résultat attendu

Android demande l'autorisation d'accéder aux contacts.

---

## 14.02 — Lire les contacts

### Résultat attendu

L'application peut récupérer les contacts autorisés.

---

## 14.03 — Créer `ContactResolver`

### Résultat attendu


Thomas
 ↓
Thomas Dupont


---

## 14.04 — Aucun contact

### Résultat attendu


"Je ne trouve aucun Thomas."


---

## 14.05 — Plusieurs contacts

### Résultat attendu


Thomas Dupont
Thomas Martin


L'assistant demande lequel choisir.

---

# PHASE 15 — Appel sortant

## 15.01 — Créer `CALL_CONTACT`

### Résultat attendu


CALL_CONTACT("Thomas")


---

## 15.02 — Résoudre le contact

### Résultat attendu


Thomas
 ↓
Thomas Dupont
 ↓
Numéro


---

## 15.03 — Demander les permissions nécessaires

### Résultat attendu

L'application sait si elle a les permissions nécessaires.

---

## 15.04 — Créer `CallManager`

### Résultat attendu

La gestion des appels est séparée du parser.

---

## 15.05 — Lancer un appel

### Résultat attendu

Le téléphone commence l'appel.

---

## 15.06 — Ajouter confirmation

### Résultat attendu


"Appelle Thomas"
 ↓
"J'appelle Thomas Dupont ?"
 ↓
"Oui"
 ↓
📞 Appel


---

# PHASE 16 — Appel entrant

## 16.01 — Étudier les APIs Telecom

Étudier notamment :


TelecomManager
InCallService
RoleManager


### Résultat attendu

Comprendre quelles APIs et quels rôles Android sont nécessaires pour gérer les appels.

---

## 16.02 — Définir les états


NO_CALL
INCOMING_CALL
ACTIVE_CALL
CALL_ENDED


### Résultat attendu

L'application sait dans quel état se trouve l'appel.

---

## 16.03 — Détecter un appel

### Résultat attendu

Lorsqu'un téléphone reçoit un appel :


NO_CALL
 ↓
INCOMING_CALL


---

## 16.04 — Identifier l'appelant

### Résultat attendu

Si le numéro appartient à un contact :


Appel entrant
 ↓
Thomas Dupont


---

# PHASE 17 — Répondre / refuser

## 17.01 — Préparer le rôle téléphonique

### Résultat attendu

L'application sait si elle dispose du rôle nécessaire.

---

## 17.02 — Créer `ANSWER_CALL`

### Résultat attendu


"réponds"
"décroche"
"accepte"


produisent :


ANSWER_CALL


---

## 17.03 — Implémenter réponse

### Résultat attendu

Un appel entrant peut être accepté.

---

## 17.04 — Créer `REJECT_CALL`

### Résultat attendu


"refuse"
"rejette l'appel"
"raccroche"


produisent :


REJECT_CALL


---

## 17.05 — Implémenter refus

### Résultat attendu

Un appel entrant peut être rejeté.

---

# PHASE 18 — Messages

## 18.01 — Créer `SEND_MESSAGE`

### Résultat attendu


SEND_MESSAGE


existe comme Intent.

---

## 18.02 — Extraire le destinataire

Phrase :

> Envoie un message à Thomas.

### Résultat attendu


contact = Thomas


---

## 18.03 — Extraire le message

Phrase :

> Envoie à Thomas : je suis arrivé.

### Résultat attendu


contact = Thomas
message = "je suis arrivé"


---

## 18.04 — Demander confirmation

### Résultat attendu


"Je vais envoyer à Thomas : je suis arrivé. Confirmer ?"


---

## 18.05 — Envoyer

### À faire

- [ ] Vérifier les APIs Android disponibles.
- [ ] Vérifier les permissions.
- [ ] Implémenter l'envoi selon le mécanisme retenu.

### Résultat attendu

Le message est envoyé uniquement lorsque les conditions nécessaires sont remplies.

---

# PHASE 19 — Musique avancée

## 19.01 — Créer `PLAY_SONG`

### Résultat attendu

Le système peut représenter :


PLAY_SONG("Nom de la musique")


---

## 19.02 — Créer `PLAY_PLAYLIST`

### Résultat attendu


PLAY_PLAYLIST("Ma playlist")


---

## 19.03 — Détecter le nom

Phrase :

> Lance ma playlist détente.

### Résultat attendu


playlist = "détente"


---

## 19.04 — Connecter au lecteur

### Résultat attendu

L'assistant utilise les mécanismes réellement disponibles dans l'application musicale cible.

---

# PHASE 20 — Langage naturel simple

## 20.01 — Ajouter des synonymes

Exemple :


pause
stop
arrête
mets en pause


### Résultat attendu

Tous sont compris comme :


PAUSE


---

## 20.02 — Ajouter des formulations familières

Exemple :


mets la suivante
passe
skip


### Résultat attendu

Compréhension améliorée sans IA.

---

## 20.03 — Corriger les petites différences

Gérer :


"mets pause"
"met pause"
"met en pause"


### Résultat attendu

Les formulations proches sont regroupées.

---

# PHASE 21 — Contexte conversationnel

## 21.01 — Stocker la dernière commande

### Résultat attendu

L'assistant sait ce qui vient d'être demandé.

---

## 21.02 — Confirmation "oui"

Conversation :


Appelle Thomas.
Thomas Dupont ?
Oui.


### Résultat attendu

Le "Oui" confirme l'action précédente.

---

## 21.03 — Confirmation "non"

### Résultat attendu


Non
 ↓
Action annulée


---

## 21.04 — Choix entre plusieurs contacts

### Résultat attendu


"Le premier"


est interprété dans le contexte de la question précédente.

---

# PHASE 22 — Système de confirmation

## 22.01 — Définir les niveaux


LOW_RISK
MEDIUM_RISK
HIGH_RISK


---

## 22.02 — Actions sans confirmation

Par exemple :

- [ ] Play
- [ ] Pause
- [ ] Next
- [ ] Previous
- [ ] Volume

### Résultat attendu

Ces commandes sont rapides.

---

## 22.03 — Actions nécessitant confirmation

Par exemple :

- [ ] Appeler
- [ ] Envoyer un message
- [ ] Autres actions sensibles

### Résultat attendu

L'action n'est pas exécutée avant confirmation.

---

# PHASE 23 — Plusieurs commandes

## 23.01 — Deux commandes

Phrase :

> Lance la musique et ouvre Discord.

### Résultat attendu


PLAY
OPEN_APP("Discord")


---

## 23.02 — Trois commandes

Phrase :

> Lance la musique, monte le son et ouvre Discord.

### Résultat attendu


PLAY
VOLUME_UP
OPEN_APP("Discord")


---

## 23.03 — Exécution dans l'ordre

### Résultat attendu

Les actions sont exécutées dans l'ordre où elles ont été demandées.

---

# PHASE 24 — Fonctionnement en arrière-plan

## 24.01 — Étudier les contraintes Android

### À faire

- [ ] Comprendre les services en arrière-plan.
- [ ] Comprendre les restrictions batterie.
- [ ] Identifier le mécanisme adapté au projet.

### Résultat attendu

Tu sais comment maintenir les fonctions nécessaires sans créer un service inutilement lourd.

---

## 24.02 — Créer le service nécessaire

### Résultat attendu

L'assistant peut maintenir les composants nécessaires en arrière-plan.

---

## 24.03 — Tester en changeant d'application

### Résultat attendu

L'assistant reste disponible lorsque l'utilisateur ouvre une autre application.

---

# PHASE 25 — Wake Word

> Cette phase arrive volontairement tard. Le reste de l'assistant doit déjà fonctionner.

## 25.01 — Choisir le Wake Word

Exemple :


OK ADO


### Résultat attendu

Un mot d'activation est défini.

---

## 25.02 — Choisir une solution de détection

### À faire

- [ ] Rechercher une solution adaptée à Android.
- [ ] Vérifier si elle fonctionne localement.
- [ ] Vérifier la consommation batterie.
- [ ] Vérifier la licence.

### Résultat attendu

Une solution réaliste est sélectionnée.

---

## 25.03 — Détecter le Wake Word

### Résultat attendu


"OK ADO"
 ↓
Détection
 ↓
Assistant actif


---

## 25.04 — Lancer automatiquement Speech-to-Text

### Résultat attendu


"OK ADO"
 ↓
Écoute
 ↓
"Pause"
 ↓
PAUSE


---

# PHASE 26 — Écran verrouillé

## 26.01

- [ ] Tester Wake Word écran verrouillé.
- [ ] Tester commande vocale.
- [ ] Tester réponse vocale.

### Résultat attendu

Les fonctions autorisées continuent de fonctionner lorsque le téléphone est verrouillé.

---

## 26.02 — Tester les commandes sensibles

- [ ] Appel
- [ ] Réponse
- [ ] Refus
- [ ] Message

### Résultat attendu

Le comportement respecte les restrictions de sécurité Android.

---

# PHASE 27 — Fonctionnement hors ligne

## 27.01 — Identifier les dépendances réseau

- [ ] Speech-to-Text
- [ ] Wake Word
- [ ] IA
- [ ] Autres services

### Résultat attendu

Tu sais exactement quelles fonctions nécessitent Internet.

---

## 27.02 — Parser local

### Résultat attendu

Les commandes basiques fonctionnent sans réseau.

---

## 27.03 — TTS local

### Résultat attendu

L'assistant peut répondre vocalement sans connexion si le moteur vocal installé le permet.

---

## 27.04 — Reconnaissance locale

### À faire

- [ ] Évaluer un moteur local adapté.
- [ ] Tester précision.
- [ ] Tester consommation.
- [ ] Tester vitesse.

### Résultat attendu

Une solution locale viable est choisie si elle répond aux besoins.

---

# PHASE 28 — IA optionnelle

> L'IA est un ajout. Elle ne doit pas devenir une dépendance obligatoire pour les commandes simples.

## 28.01 — Définir un format d'Intent

Exemple :


{
  "intent": "CALL_CONTACT",
  "contact": "Thomas"
}


### Résultat attendu

L'IA produit des données structurées plutôt qu'une commande Android directe.

---

## 28.02 — Valider l'Intent

### À faire

- [ ] Vérifier l'Intent.
- [ ] Vérifier les paramètres.
- [ ] Vérifier les valeurs.
- [ ] Vérifier les permissions.

### Résultat attendu

Une réponse IA incorrecte ne peut pas directement exécuter une action dangereuse ou invalide.

---

## 28.03 — Ajouter confirmation

### Résultat attendu

Les actions sensibles passent toujours par le système de confirmation.

---

## 28.04 — Fallback sans IA

### Résultat attendu

Si l'IA est indisponible :


Commande simple
 ↓
Parser classique
 ↓
Action


continue de fonctionner.

---

# PHASE 29 — Historique

## 29.01 — Créer le modèle

Stocker :


date
commande
intent
résultat


### Résultat attendu

Une commande peut être enregistrée.

---

## 29.02 — Afficher l'historique

### Résultat attendu

L'utilisateur peut voir les dernières commandes.

---

## 29.03 — Supprimer l'historique

- [ ] Supprimer une entrée.
- [ ] Tout supprimer.

### Résultat attendu

L'utilisateur garde le contrôle de ses données.

---

# PHASE 30 — Paramètres

## 30.01 — Créer l'écran paramètres

### Résultat attendu

Un écran dédié aux réglages existe.

---

## 30.02 — Paramètres vocaux

- [ ] Langue
- [ ] Voix
- [ ] Vitesse
- [ ] Volume de réponse

### Résultat attendu

La réponse vocale est configurable.

---

## 30.03 — Paramètres Wake Word

- [ ] Activer
- [ ] Désactiver

### Résultat attendu

Le Wake Word peut être coupé sans désinstaller l'application.

---

## 30.04 — Paramètres de confidentialité

- [ ] Historique
- [ ] Permissions
- [ ] Traitement local
- [ ] Services réseau

### Résultat attendu

L'utilisateur sait ce que l'assistant utilise.

---

# PHASE 31 — Gestion des erreurs

## 31.01 — Commande inconnue

### Résultat attendu


"Je n'ai pas compris."


---

## 31.02 — Permission manquante

### Résultat attendu


"J'ai besoin de l'autorisation nécessaire pour faire cela."


---

## 31.03 — Application inexistante

### Résultat attendu


"Je ne trouve pas cette application."


---

## 31.04 — Contact inexistant

### Résultat attendu


"Je ne trouve pas ce contact."


---

## 31.05 — Fonction indisponible

### Résultat attendu

L'assistant explique que l'action n'est pas disponible au lieu de planter.

---

# PHASE 32 — Tests unitaires

## 32.01 — Tester le parser

- [ ] PLAY
- [ ] PAUSE
- [ ] NEXT
- [ ] PREVIOUS
- [ ] OPEN_APP
- [ ] CALL_CONTACT
- [ ] ANSWER_CALL
- [ ] REJECT_CALL
- [ ] SEND_MESSAGE
- [ ] UNKNOWN

### Résultat attendu

Chaque commande produit l'Intent attendu.

---

## 32.02 — Tester les paramètres

- [ ] Nom application
- [ ] Nom contact
- [ ] Nom playlist
- [ ] Nom musique
- [ ] Texte message
- [ ] Volume

### Résultat attendu

Les paramètres sont correctement extraits.

---

# PHASE 33 — Tests réels

## 33.01 — Test téléphone

- [ ] Application ouverte
- [ ] Application en arrière-plan
- [ ] Écran éteint
- [ ] Écran verrouillé

### Résultat attendu

Les fonctions prévues restent disponibles.

---

## 33.02 — Test musique

- [ ] Play
- [ ] Pause
- [ ] Next
- [ ] Previous
- [ ] Volume
- [ ] Playlist

### Résultat attendu

Toutes les commandes supportées fonctionnent.

---

## 33.03 — Test appels

- [ ] Appel sortant
- [ ] Appel entrant
- [ ] Répondre
- [ ] Refuser
- [ ] Contact connu
- [ ] Numéro inconnu

### Résultat attendu

Chaque scénario possède un comportement maîtrisé.

---

## 33.04 — Test messages

- [ ] Contact connu
- [ ] Contact inconnu
- [ ] Message court
- [ ] Message long
- [ ] Confirmation
- [ ] Annulation

### Résultat attendu

Les messages ne sont jamais envoyés par erreur.

---

# PHASE 34 — Tests de sécurité

## 34.01 — Permissions

- [ ] Microphone refusé
- [ ] Contacts refusés
- [ ] Téléphone refusé
- [ ] Permissions nécessaires aux messages refusées

### Résultat attendu

L'application reste utilisable sans crash.

---

## 34.02 — Confirmation

- [ ] Appel sans confirmation
- [ ] Message sans confirmation
- [ ] Action annulée

### Résultat attendu

Une action sensible ne doit pas être déclenchée par une interprétation ambiguë.

---

# PHASE 35 — Batterie

## 35.01 — Mesurer au repos

### Résultat attendu

Connaître la consommation lorsque l'assistant ne fait rien.

---

## 35.02 — Mesurer Mot Magique

### Résultat attendu

Connaître le coût du Mot Magique.

---

## 35.03 — Optimiser

- [ ] Réduire les traitements inutiles.
- [ ] Libérer les ressources.
- [ ] Éviter plusieurs moteurs audio simultanés.

### Résultat attendu

L'assistant reste raisonnable en consommation.

---

# PHASE 36 — Performance

## 36.01 — Mesurer la reconnaissance

### Résultat attendu

Connaître le temps :


Parole → Texte


---

## 36.02 — Mesurer le parsing

### Résultat attendu

Connaître le temps :


Texte → Intent


---

## 36.03 — Mesurer l'exécution

### Résultat attendu

Connaître le temps :


Intent → Action


---

## 36.04 — Optimiser

### Résultat attendu

Le délai total est suffisamment faible pour donner une impression de réponse immédiate.

---

# PHASE 37 — Nettoyage du projet

## 37.01

- [ ] Supprimer le code temporaire.
- [ ] Supprimer les tests manuels inutiles.
- [ ] Supprimer les dépendances inutiles.
- [ ] Corriger les warnings.
- [ ] Renommer les classes si nécessaire.

### Résultat attendu

Le projet est propre.

---

## 37.02 — Vérifier l'architecture

### Résultat attendu


Voice
  ↓
NLP
  ↓
Intent
  ↓
Executor
  ↓
Android / Services


Les responsabilités restent séparées.

---

# PHASE 38 — Documentation

## 38.01 — Documenter l'architecture

- [ ] Diagramme global
- [ ] Packages
- [ ] Classes principales

### Résultat attendu

Quelqu'un peut comprendre comment le projet fonctionne.

---

## 38.02 — Documenter les commandes

Créer une liste :


"Lance la musique"
"Pause"
"Suivante"
"Précédente"
"Ouvre Discord"
"Appelle Thomas"
"Réponds"
"Refuse"
"Envoie un message..."


### Résultat attendu

Toutes les commandes supportées sont documentées.

---

# PHASE 39 — Version MVP

Le MVP doit rester volontairement simple.

## Fonctionnalités

- [ ] Microphone
- [ ] Speech-to-Text
- [ ] Text-to-Speech
- [ ] PLAY
- [ ] PAUSE
- [ ] NEXT
- [ ] PREVIOUS
- [ ] Volume
- [ ] Ouverture d'application
- [ ] Contacts
- [ ] Appel
- [ ] Réponse appel
- [ ] Refus appel
- [ ] Message
- [ ] Confirmation
- [ ] Gestion des erreurs

### Résultat attendu

Tu possèdes déjà un assistant personnel utilisable sans avoir besoin d'IA.

---

# PHASE 40 — Version avancée

Ajouter progressivement :

- [ ] Wake Word
- [ ] Arrière-plan
- [ ] Écran verrouillé
- [ ] Fonctionnement hors ligne
- [ ] Contexte
- [ ] Commandes multiples
- [ ] Playlist
- [ ] Historique
- [ ] Paramètres avancés

### Résultat attendu

L'assistant commence à se rapprocher d'un véritable assistant vocal personnel.

---

# PHASE 41 — IA optionnelle finale

- [ ] Ajouter une IA locale ou distante
- [ ] Compréhension de formulations complexes
- [ ] Extraction structurée des paramètres
- [ ] Validation
- [ ] Confirmation
- [ ] Fallback sans IA
- [ ] Tests d'ambiguïté

### Résultat attendu

L'IA améliore la compréhension sans devenir indispensable au fonctionnement de base.

---

# 🏁 CHECKLIST FINALE

## Fondation

- [ ] Projet créé
- [ ] Projet compilable
- [ ] Git configuré
- [ ] Architecture créée
- [ ] Interface créée

## Voix

- [ ] Microphone
- [ ] Speech-to-Text
- [ ] Text-to-Speech
- [ ] Wake Word
- [ ] Fonctionnement arrière-plan
- [ ] Écran verrouillé

## Musique

- [ ] Play
- [ ] Pause
- [ ] Suivant
- [ ] Précédent
- [ ] Volume
- [ ] Musique spécifique
- [ ] Playlist

## Applications

- [ ] Détection
- [ ] Recherche
- [ ] Ouverture

## Contacts / téléphone

- [ ] Contacts
- [ ] Appel sortant
- [ ] Appel entrant
- [ ] Répondre
- [ ] Refuser

## Messages

- [ ] Destinataire
- [ ] Texte
- [ ] Confirmation
- [ ] Envoi

## Intelligence

- [ ] Intent
- [ ] Parser
- [ ] Contexte
- [ ] Clarification
- [ ] Commandes multiples
- [ ] IA optionnelle

## Qualité

- [ ] Gestion des erreurs
- [ ] Tests unitaires
- [ ] Tests réels
- [ ] Tests sécurité
- [ ] Batterie
- [ ] Performance
- [ ] Documentation

---


**README.md généré majoritèrement par ChatGPT.**
