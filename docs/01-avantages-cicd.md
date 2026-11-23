 6 avantages de la CI/CD

 1. Qualité
 Concret : À chaque `git push`, les tests se lancent tout seuls et bloquent le code s'il y a un bug
 Exemple : Dans le module IDC, les tests automatiques sur GitHub ont bloqué une Pull Request parce qu'une route API était cassée
 Mesure : Pourcentage de mises à jour qui cassent quelque chose en production (taux d'échec)

 2. Vitesse
 Concret : Le build Docker et la mise en ligne se font automatiquement en un clic au lieu de prendre des heures à la main
 Exemple : En 2009, Flickr est passé à plus de 10 mises en ligne par jour grâce aux déploiements en un clic
 Mesure : Temps entre le `git commit` et la mise en ligne

 3. Fiabilité
 Concret : Le robot exécute toujours les mêmes commandes sans rien oublier, et on peut annuler une mise à jour en 2 minutes si ça plante
 Exemple : En 2012, Knight Capital a oublié 1 serveur sur 8 lors d'une mise à jour manuelle et a perdu 440M $ en 45 minutes
 Mesure : Temps moyen pour réparer le site après un crash (MTTR)

 4. Sécurité
 Concret : Un scanner vérifie automatiquement qu'il n'y a pas de faille ni de mot de passe oublié dans le code avant de valider
 Exemple : Dans le module IDC, Semgrep a bloqué une Pull Request tout seul après avoir trouvé une faille XSS
 Mesure : Nombre de failles de sécurité (CVE) détectées et temps pour les corriger

 5. Coût
 Concret : Personne n'a besoin de rester devant son PC pour lancer les mises à jour manuellement
 Exemple : Amazon lance une mise en ligne toutes les 11,6 secondes sans intervention humaine
 Mesure : Nombre d'heures passées à gérer les déploiements

 6. Humain
 Concret : Les développeurs n'ont plus peur de tout casser en mettant en ligne, ce qui enlève le stress et les conflits dans l'équipe
 Exemple : Chez Etsy, même un stagiaire ou un nouveau développeur met du code en ligne dès son premier jour
 Mesure : Temps mis par un nouveau développeur pour faire sa première mise en ligne

-----------------------------------------------

 Deux limites ou risques de la CI/CD

 - Diffuser un bug partout instantanément
Si les tests sont insuffisants, l'automatisation va déployer une erreur sur tous les serveurs en même temps au lieu de toucher une seule machine. 
Pour éviter ce risque, il faut faire des déploiements progressif, surveiller l'application en continu et automatiser le retour arrière (rollback) en cas d'alerte.

 - Ralentir les développeurs avec une pipeline trop lourde
Multiplier les vérifications (lint, tests, sécurité, build Docker) peut rendre la CI très lente à chaque git push et bloquer l'avancement de l'équipe. 
Pour mitiger ce problème, il faut mettre en cache les dépendances, lancer les tâches en parallèle et réserver les analyses les plus longues uniquement à la branche main.

------------------------------------------------

Pour notre projet d'équipe (epf-app), nous visons en priorité trois avantages : 

- la fiabilité en automatisant l'infrastructure avec Terraform et le déploiement avec Ansible pour éviter les erreurs manuelles
- la qualité et la sécurité en bloquant automatiquement les bugs et failles dès les Pull Requests
- la vitesse en publiant nos images Docker sur GHCR via des tags
