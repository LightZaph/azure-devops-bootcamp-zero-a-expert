## 1. Création d'un Compte Azure

Pour commencer à utiliser Azure, vous devez disposer d'un compte. Plusieurs options s'offrent à vous selon votre situation .

### Compte Gratuit (Free Account)

Le **Azure free account** est l'option idéale pour les étudiants, les développeurs ou toute personne souhaitant découvrir la plateforme sans engagement financier .

**Ce qui est inclus :**
- **Crédit de 300 $** : valable 30 jours pour explorer n'importe quel service Azure 
- **Services populaires gratuits pendant 12 mois** : comme les machines virtuelles (Linux/Windows), le stockage Blob, ou Azure SQL Database 
- **Plus de 55 services toujours gratuits** : Azure Functions, Azure DevOps, Conteneurs, etc. 

**Limites :**
- Un seul compte gratuit par client 
- Nécessite une carte de crédit (ou de débit) pour la vérification d'identité (une pré-autorisation temporaire de 1 $ est effectuée, mais aucun débit n'est réalisé) 
- Disponible dans plus de 140 pays 

### Compte Pay-As-You-Go

Le modèle **pay-as-you-go** (paiement à l'utilisation) est le mode de facturation standard d'Azure .

**Caractéristiques :**
- Pas d'engagement initial 
- Vous payez uniquement ce que vous consommez au-delà des quotas gratuits 
- Possibilité d'annuler à tout moment 
- Accès à tous les services Azure sans restriction 

**Transition :** Vous pouvez commencer avec un compte gratuit et passer en **pay-as-you-go** après 30 jours ou après avoir utilisé votre crédit de 200 $. Si vous ne faites pas cette transition, vos services seront désactivés .

### Processus d'inscription

Pour créer un compte Azure, vous aurez besoin de  :
1. Un numéro de téléphone (vérification)
2. Une carte de crédit ou de débit (validation d'identité)
3. Un compte Microsoft **ou** un compte GitHub

> **Point clé à retenir** : Le compte gratuit vous permet de **"apprendre sans payer"** avec des ressources limitées. Le **pay-as-you-go** est le modèle standard pour la production, facturé à la consommation réelle.

---

## 2. Infrastructure Globale Azure : Régions et Zones de Disponibilité

Azure possède plus de 60 régions dans le monde, réparties sur tous les continents . Cette présence mondiale répond à deux objectifs majeurs : réduire la **latence** et assurer la **disponibilité** (uptime).

### Datacenters et Latence

Le **public cloud** (Azure, AWS, GCP) met à disposition des serveurs (CPU, RAM, storage, network) dans des **datacenters** répartis géographiquement .  
Pourquoi ? Si vos utilisateurs sont en France, il est préférable que leurs données soient hébergées dans un datacenter à Paris plutôt qu'aux États-Unis, afin d'éviter la **latence** (temps de réponse élevé). Azure possède des datacenters en **France**, en **Allemagne**, etc. 

### Régions (Regions)

Une **région Azure** est une zone géographique contenant un ou plusieurs datacenters, reliés par un réseau à faible latence .

**Exemples concrets :**
- **USA** : On distingue *US West* (Californie), *US East* (Virginie), *US Central* (Texas, Iowa, etc.) 
- **Europe** : *France Central* (Paris), *Germany West Central* (Francfort)
- **Asie** : *Southeast Asia* (Singapour), *Japan East* (Tokyo)

> **Pourquoi plusieurs régions aux USA ?** Pour éviter la latence et les temps d'arrêt (downtime). Un utilisateur à Los Angeles se connectera à *US West*, un utilisateur à New York à *US East*.

### Zones de Disponibilité (Availability Zones)

Une **Availability Zone** est un emplacement physique séparé **au sein d'une région**. Chaque zone est constituée d'un ou plusieurs datacenters avec une alimentation électrique, un refroidissement et un réseau indépendants .

**Caractéristiques clés :** 
- Minimum de **3 zones distinctes** par région supportée
- Distance physique suffisante pour survivre à une catastrophe locale (incendie, inondation)
- Connectées par un réseau haute performance avec une latence **< 2 ms** 

### Relation Région / Zone

Voici la hiérarchie à retenir :

```
Géographie (ex: Amérique du Nord)
    └── Région (ex: East US)
          ├── Availability Zone 1 (Datacenter A)
          ├── Availability Zone 2 (Datacenter B)
          └── Availability Zone 3 (Datacenter C)
```

**Exemple d'architecture résiliente :**
Pour garantir une **haute disponibilité (HA)** , on déploie une application sur plusieurs VM réparties dans différentes **Availability Zones** au sein d'une même région. Si une zone tombe en panne, les autres continuent de fonctionner .

> **Termes techniques associés :** On parle de **zonal services** (ressources attachées à une zone spécifique, comme une VM) et de **zone-redundant services** (ressources automatiquement répliquées entre zones, comme le stockage Azure) .

---

## 3. Les Modèles de Service Cloud

Le cloud computing se décline en trois principaux modèles de service, définissant le niveau de responsabilité partagé entre le fournisseur et le client .

### IaaS (Infrastructure as a Service)

L'**IaaS** fournit des ressources informatiques virtualisées à la demande : serveurs, stockage, réseaux. C'est le modèle qui se rapproche le plus de l'infrastructure traditionnelle .

**Géré par Azure :** Matériel, réseau physique, virtualisation   
**Géré par vous :** OS, applications, configurations, sécurité logicielle 

**Exemples Azure IaaS :**
- **Azure Virtual Machines** (VMs) 
- Azure Virtual Network (VNet)
- Azure Disk Storage

**Quand l'utiliser ?** Pour migrer des applications existantes (legacy) sans les modifier, ou pour avoir un contrôle total sur l'environnement.

### PaaS (Platform as a Service)

Le **PaaS** fournit une plateforme complète pour développer, déployer et gérer des applications, sans la complexité de gérer l'infrastructure sous-jacente .

**Géré par Azure :** Infrastructure + OS + mises à jour + middleware   
**Géré par vous :** Code applicatif, données 

**Exemples Azure PaaS :**
- **Azure SQL Database** 
- Azure App Service (hébergement web)
- Azure Functions (serverless)

**Quand l'utiliser ?** Pour se concentrer sur le développement d'applications sans gérer les serveurs ni les licences. Idéal pour les développeurs .

### SaaS (Software as a Service)

Le **SaaS** fournit des applications logicielles complètes, prêtes à l'emploi, accessibles via Internet .

**Géré par Azure :** Tout (infrastructure, plateforme, application, données)   
**Géré par vous :** Rien (simple utilisation) 

**Exemples Azure SaaS :**
- **Office 365** (Outlook, Word, Excel) 
- Dynamics 365
- Azure DevOps

### Tableau Récapitulatif et Exemples Concrets

| Modèle | Vous gérez | Fournisseur gère | Exemples Azure |
| :--- | :--- | :--- | :--- |
| **IaaS** | OS, apps, runtime, données | Virtualisation, serveurs, stockage, réseau | **VM**, Disques, Réseaux  |
| **PaaS** | Apps, données | OS, runtime, middleware, infrastructure | **Azure SQL Database**, App Service  |
| **SaaS** | Rien (utilisation) | Application, données, plateforme, infrastructure | **Outlook**, **Office 365**, Dynamics 365  |

> **Règle simple pour retenir :**
> - **VM** = **IaaS** (on installe tout)
> - **Base de données** (Azure SQL) = **PaaS** (on écrit juste les requêtes)
> - **Application web métier** (Outlook) = **SaaS** (on clique et on utilise)

---

**Ce qu'il faut retenir pour la pratique :**
1. On crée un **compte gratuit** pour apprendre, on passe en **pay-as-you-go** pour produire.
2. Les **Régions** évitent la latence et les pannes, les **Availability Zones** évitent la panne.
3. **IaaS** = contrôle maximal (VM), **PaaS** = productivité développeur (Base de données), **SaaS** = solution clé en main (Office 365).