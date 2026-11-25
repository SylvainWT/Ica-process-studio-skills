---
name: dummy-process-studio-ping
description: Use when the user wants to test the connection between Bob and Process Studio, or asks to run the "dummy skill", "ping Process Studio" or "test skill" — a harmless placeholder skill that returns a deterministic confirmation.
---

# Dummy Process Studio Ping

Skill factice (dummy) destiné à vérifier que Process Studio découvre, charge et exécute correctement un skill. Il ne modifie aucun fichier et n'appelle aucun service externe.

## Procédure

1. Annonce à l'utilisateur : `[dummy-process-studio-ping] Skill activé.`
2. Récupère le contexte d'exécution minimal :
   - Date/heure courante (depuis `environment_details`).
   - Mode courant (Agent, Plan, Ask…).
   - Répertoire de travail (workspace).
3. Si l'utilisateur a fourni un message ou un paramètre après la commande, répète-le tel quel dans le champ `echo`.
4. Réponds avec le bloc de confirmation ci-dessous, en remplaçant les valeurs entre `<>` :

```json
{
  "skill": "dummy-process-studio-ping",
  "version": "0.1.0",
  "status": "ok",
  "timestamp": "<date-heure courante>",
  "mode": "<mode courant>",
  "workspace": "<chemin du workspace>",
  "echo": "<message de l'utilisateur ou null>",
  "checks": {
    "skill_discovered": true,
    "skill_loaded": true,
    "skill_executed": true
  }
}
```

5. Termine par une phrase : « Connexion de test avec Process Studio : OK ».

## Contenu de référence (données factices)

Exemple de processus fictif que Process Studio peut utiliser pour valider un échange de données :

| Étape | Nom                    | Responsable | Statut     |
|-------|------------------------|-------------|------------|
| 1     | Réception de la demande | Service A   | Terminé    |
| 2     | Validation             | Service B   | En cours   |
| 3     | Approbation            | Direction   | À faire    |
| 4     | Clôture                | Service A   | À faire    |

Si l'utilisateur demande « avec données », ajoute ce tableau à la réponse.

## Règles

- Ne jamais modifier de fichier ni exécuter de commande.
- Ne jamais inventer de résultat : toutes les valeurs du bloc JSON doivent provenir du contexte réel, sauf `checks` qui est fixe.
- Si un champ est indisponible, mettre `null`.
