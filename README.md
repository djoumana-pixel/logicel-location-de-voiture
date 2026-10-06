# ABT Location — logiciel de gestion (Étape 1)

## Installation (Windows / Linux / Mac)
```bash
python -m venv venv
# Windows :  venv\Scripts\activate        Linux/Mac :  source venv/bin/activate
pip install -r requirements.txt
python manage.py makemigrations accounts vehicles clients reservations finance
python manage.py migrate
python manage.py createsuperuser      # ce compte = SUPER ADMIN (accès finance)
python manage.py runserver
```
Ouvrir http://127.0.0.1:8000 → connexion.

## Rôles
- **Super admin** : tout + finance + prix d'achat + coûts d'entretien + gestion des utilisateurs (/admin).
- **Admin / Employé** : véhicules, clients, réservations. Ils ne voient AUCUN montant de finance.

## Règles finance (source unique : apps/finance/services.py)
- Revenu = paiements réellement encaissés (par date de paiement).
- La caution n'est jamais un revenu.
- Dépense = toutes les dépenses ; un entretien avec coût crée automatiquement sa dépense (pas de double saisie).
- Bénéfice = revenus - dépenses.
- Supprimer une voiture avec historique = archivage (la finance reste exacte). Sans historique = suppression définitive.
- Chaque modification est historisée (qui / quand) via django-simple-history.

## Contrat Word
`docs/contrat_template.docx` (champs {{ ... }}) — génération automatique à l'étape 3.

## Suite
2. Clients + Réservations + Paiements  3. Contrat Word  4. Finance + Dashboard + Calendrier  5. Historique + déploiement
