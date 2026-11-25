# Standard d'exigence — UCQCS v4.8 (Unified Code Quality Control System)

> UCQCS et CI Unified sont une seule et même chose : le workflow réutilisable `g33ky00/.github/.github/workflows/ucqcs.yml` est le moteur UCQCS, et le caller dans chaque repo s'appelle `ci-unified.yml`. Les deux termes sont interchangeables.

## Principes fondamentaux
- **Langue** : l'anglais est utilisé absolument partout dans les écrits sur GitHub (README, commits, issues, PRs, workflows, documentation).
- **About** : le bloc "About" de chaque projet doit être dûment complété (description, topics, homepage).
- **Licences** : dépôts privés → GNU Affero General Public License v3 (AGPL-3.0) ; dépôts publics → MIT License.
- **Forks** : les dépôts de type "fork" ne sont PAS traités par UCQCS (nous n'en sommes pas responsables). Ils sont exclus de la flotte UCQCS.
- **Terminologie** : UCQCS = CI Unified. Aucune confusion tolérée entre les deux termes.
## Niveau de sécurité (bloquant)
- **Secrets scan** (gitleaks) : aucun secret en clair dans le code ou l'historique
- **SAST** (Semgrep CE sur tous les repos + Strix quick sur PR) : aucun finding critique/high
- **Dépendances** : aucune CVE critique non corrigée (Dependabot)
- **Outils gratuits OSS** : gitleaks, Semgrep CE, bandit, gosec, brakeman, phpstan, cargo audit, bundler-audit, pip-audit, npm audit

## Niveau de compliance rédactionnelle (bloquant)
- README.md avec sections : About, Structure, Stack, Contributing, License
- Badge CI shields.io
- Pas d'IP, chemins serveur, ou secrets dans le README
- Versions cohérentes (README = package.json/go.mod/etc.)
- Fichiers référencés existent localement
- Fichier LICENSE présent si référencé

## Niveau de qualité de code (progressif)
- Formatage : gofmt, ruff format, cargo fmt, prettier (bloquant)
- Linting : eslint, ruff check, golangci-lint (bloquant)
- Type checking : tsc --noEmit, mypy (bloquant)
- Vulnérabilités dépendances : npm audit, pip-audit, cargo audit (bloquant)
- SAST multi-langage : Semgrep CE (30+ langages, gratuit, remplace CodeQL sur privés)

## Niveau de tests (progressif)
- Tests unitaires exécutés sur chaque PR
- Couverture minimale : 60% (objectif 80%)

## Calendrier d'implémentation
- **Niveau 1** : GO immédiat (secrets, CVE critiques, formatage, build, Semgrep, Strix quick)
- **Niveau 2** : J+15 (linting, type checking, Strix quick, couverture 60%)
- **Niveau 3** : J+45 (couverture 80%, Strix deep, documentation)
- **Niveau 4** : J+60 (couverture 90%, performance benchmarks)

## Workflows requis par repo
- `ci-unified.yml` → UCQCS v4.8+ (reusable depuis g33ky00/.github)
- `strix-quick.yml` → Strix scan sur PR + rapport complet sur erreur
- `strix-deep.yml` → Strix scan hebdomadaire (lundi 3h)
- `dependabot.yml` → mises à jour hebdomadaires github-actions

## Limitations GitHub gratuit (repos privés)
- Pas de SARIF upload (GHAS payant) → utiliser $GITHUB_STEP_SUMMARY + ::error:: + artifacts
- Pas de CodeQL (GHAS payant) → Semgrep CE
- Pas de branch protection (Pro payant) → gérer manuellement
- 2 000 min/mois, 20 jobs concurrents, 6 h max/job, 10 Go cache/repo
