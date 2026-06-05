# GitHub Learning - Fork Ansel

## Session 1 : 2026-06-05

### Problème rencontré
Le workflow "Build and Push Docker Image" échouait avec l'erreur :
```
##[error]Username and password required
```

**Cause racine** : Le workflow tentait de se connecter à Docker Hub mais les secrets `DOCKERHUB_USERNAME` et `DOCKERHUB_TOKEN` n'étaient pas configurés dans le fork.

### Concepts appris

#### 1. Qu'est-ce que Docker ?
- **Définition** : Un outil de containerisation qui empaquette une application avec toutes ses dépendances
- **Analogie** : Un "box" qui contient tout ce nécessaire pour faire fonctionner l'application
- **Utilité** : Permet aux utilisateurs de lancer l'app sans avoir à la compiler : `docker run aurelienpierre/ansel:current`

#### 2. GitHub Actions et Workflows
- **Emplacement** : Les workflows sont définis dans `.github/workflows/` (fichiers `.yml`)
- **Déclenchement** : Peuvent s'exécuter automatiquement (sur push, schedule) ou manuellement
- **Coût** : Certains workflows (builds, Docker, tests) consomment beaucoup de ressources GitHub Actions
- **Désactivation** : Interface → Actions → ⋯ → "Disable workflow" (reste local au fork, n'affecte pas le dépôt maître)

#### 3. Branches et commits
- **Branche** : Une copie du code permettant de travailler en parallèle
- **Commit** : Une "sauvegarde" du code avec un message explicatif
- **Push** : Envoyer un commit vers le serveur GitHub
- **Revert** : Annuler un commit (proprement via `git revert` ou `reset`)

#### 4. Forks et synchronisation
- **Fork** : Une copie personnelle d'un dépôt (ici : blonchkman/ansel est un fork de aurelienpierreeng/ansel)
- **Dépôt maître/upstream** : Le dépôt original (aurelienpierreeng/ansel)
- **Isolation** : Les modifications locales du fork n'affectent JAMAIS le dépôt maître

### Actions prises

1. **Identification du problème** : Logs du workflow → erreur d'authentification Docker
2. **Compréhension** : Secrets manquants pour Docker Hub
3. **Solution choisie** : Désactiver tous les workflows (fork passif, pas de coding)
4. **Nettoyage** : Suppression de la branche `patch-1` qui contenait une modification accidentelle

### Configuration locale pour ce fork

#### Désactiver les workflows
✅ **Fait** : Tous les workflows ont été désactivés via l'interface GitHub
- Aucun coût en ressources
- Aucun impact sur le dépôt maître

#### Gérer `.gitignore` localement
```bash
# 1. Modifier .gitignore localement (ajouter .local/)
# 2. Exécuter cette commande pour "verrouiller" le fichier
git update-index --skip-worktree .gitignore

# Si tu dois revenir
git update-index --no-skip-worktree .gitignore

# Pour vérifier les fichiers en skip-worktree
git ls-files -v | grep "^S"
```

**Effet** :
- Les mises à jour du dépôt maître fusionnent sans conflit dans `.gitignore`
- Tes modifications locales (`+ .local/`) sont préservées
- Tes changements ne remontent jamais au dépôt maître

---

## Plan d'apprentissage progressif

### Phase 1 : Fondamentaux Git (à faire)
- [ ] Comprendre : commits, branches, push/pull
- [ ] Pratiquer : créer une branche, faire un commit, voir l'historique
- [ ] Commandes clés : `git log`, `git status`, `git diff`

### Phase 2 : Gestion du fork (à faire)
- [ ] Synchroniser le fork avec le dépôt maître
- [ ] Créer une branche de développement
- [ ] Faire un "pull request" (pas pour merger, juste pour voir le mécanisme)

### Phase 3 : GitHub Actions avancé (optionnel)
- [ ] Comprendre quand réactiver des workflows
- [ ] Lire les logs d'un workflow qui échoue
- [ ] Déboguer une action

### Phase 4 : Workflow réel (quand tu coderas)
- [ ] Créer une branche de feature
- [ ] Faire des commits propres
- [ ] Faire une Pull Request vers le dépôt maître

---

## Ressources

- [GitHub Docs - Forking a repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
- [GitHub Docs - GitHub Actions](https://docs.github.com/en/actions)
- [Git documentation officielle](https://git-scm.com/doc)

---

## Notes personnelles

Ce document est stocké dans `.local/` (hors versioning Git) pour rester local au fork.
À mettre à jour après chaque session d'apprentissage.
