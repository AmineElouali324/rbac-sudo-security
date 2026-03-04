# Projet : Accès sudo sécurisé sous Linux (RBAC & audit)

## Objectif
Mettre en place une politique de **sécurisation des privilèges** sous Linux en utilisant le contrôle d’accès basé sur les rôles (RBAC) et le principe du **moindre privilège**.  
Assurer la traçabilité complète des actions avec la journalisation système.

## Stratégie de sécurité
- Séparation des rôles en groupes :  
  - **Technicien support** : consultation de services et journaux, diagnostic sans modification.  
  - **Administrateur applicatif** : gestion des services applicatifs spécifiques (redémarrage, rechargement).  
  - **NOC (Centre d’Opérations Réseau)** : surveillance système et réseau uniquement.  
- Définition des commandes autorisées via **Cmnd_Alias** dans sudoers.  
- Application stricte du principe du **moindre privilège**.  
- Audit des actions avec **journalctl** et logs sudo.

## Technologies et outils
- **Linux** (Red Hat Enterprise Linux)  
- **sudo** avec configuration par fichiers dans `/etc/sudoers.d/`  
- **systemctl**, **journalctl**  
- Terminal et scripts Bash

## Mise en œuvre
1. Création des groupes et utilisateurs pour chaque rôle.  
2. Organisation des fichiers sudoers et définition des **règles sudo**.  
3. Attribution des commandes autorisées pour chaque rôle :  
   - **Technicien support** : `systemctl status`, `systemctl is-active`, `journalctl -u *`  
   - **Administrateur applicatif** : `systemctl restart`, `reload`, `status` pour services applicatifs  
   - **NOC** : `df`, `free`, `uptime`, `ss`  
4. Journalisation et audit pour toutes les actions sudo.  

## Tests réalisés
- Vérification que **les commandes autorisées s’exécutent correctement**.  
- Vérification que **les commandes non autorisées sont refusées**.  
- Analyse des logs pour **confirmer la traçabilité et le suivi des actions**.

## Résultats
- Sécurisation des accès sudo selon les rôles.  
- Respect du principe du moindre privilège.  
- Audit complet disponible via logs sudo et journalctl.  

## Contenu du repository
- `sudoers/` : fichiers de configuration sudoers pour chaque rôle  
- `scripts/` : scripts de test et commandes validées  
- `rapport/` : PDF du rapport détaillé du projet  
- `images/` : captures d’écran montrant les tests et validations  

## Perspectives
- Ajout d’autres rôles spécifiques selon l’organisation.  
- Intégration d’un système d’alerte automatique sur les commandes critiques.  
- Mise en place d’un dashboard de supervision pour visualiser les activités sudo.

---
