# Data Dictionary / Dictionnaire de données

## Table: loan_applications

| Column | Type | Nullable | Description (EN) | Description (FR) |
|---|---|---|---|---|
| application_id | STRING | No | Unique loan application identifier | Identifiant unique de la demande de prêt |
| company_name | STRING | No | Legal name of the applicant company | Nom légal de l'entreprise demanderesse |
| province | STRING | No | Canadian province or territory code | Code de province ou territoire canadien |
| industry_sector | STRING | No | Industry classification of the business | Classification sectorielle de l'entreprise |
| loan_amount | DECIMAL | **Yes** | Requested loan amount in CAD | Montant du prêt demandé en CAD |
| loan_purpose | STRING | No | Intended use of the loan funds | Utilisation prévue des fonds |
| application_date | DATE | No | Date the application was submitted | Date de soumission de la demande |
| employee_count | INTEGER | No | Number of full-time employees | Nombre d'employés à temps plein |
| years_in_business | INTEGER | No | Years since company incorporation | Années depuis l'incorporation |
| annual_revenue | DECIMAL | No | Most recent annual revenue in CAD | Chiffre d'affaires annuel le plus récent en CAD |
| credit_score | INTEGER | **Yes** | Applicant credit score (300–900) | Cote de crédit du demandeur (300–900) |
| status | STRING | No | Application status | Statut de la demande |

---

## Valid Values / Valeurs valides

### province
`AB, BC, MB, NB, NL, NS, NT, NU, ON, PE, QC, SK, YT`

### status
`Approved`, `Rejected`, `Under Review`

### industry_sector
`Agriculture`, `Construction`, `Energy`, `Food & Beverage`, `Forestry`, `Healthcare`, `Hospitality`, `Manufacturing`, `Mining`, `Professional Services`, `Retail`, `Services`, `Technology`, `Transportation`

---

## Data Quality Rules / Règles de qualité des données

| Rule | Field | Condition |
|---|---|---|
| Completeness | application_id | Must not be null |
| Completeness | company_name | Must not be null |
| Completeness | province | Must not be null |
| Completeness | loan_amount | Must not be null ⚠️ |
| Consistency | province | Must be a valid Canadian province/territory code |
| Consistency | loan_amount | Must be > 0 |
| Consistency | credit_score | Must be between 300 and 900 |
| Consistency | application_date | Must not be a future date |
| Uniqueness | application_id | Must be unique per batch |

> ⚠️ Known nulls exist in sample data — intentional for DQ testing purposes.

---

## Source / Source

Simulated dataset representing Canadian SMB loan applications. Inspired by publicly available Statistics Canada SME financing data.