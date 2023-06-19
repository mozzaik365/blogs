# Guide pas-à-pas pour synchroniser les profils utilisateurs entre Azure Active Directory et le Profil Utilisateur de SharePoint Online

L'intégration entre Microsoft Azure Active Directory (Azure AD) et SharePoint Online permet de centraliser la gestion des utilisateurs au sein d'une organisation. Lorsque vous utilisez ces services conjointement, il peut être utile de synchroniser des propriétés spécifiques des utilisateurs entre **Azure Active Directory** et le **Profil utilisateur SharePoint Online**. Dans cet article, nous vous guiderons à travers les étapes nécessaires pour synchroniser une propriété utilisateur entre Azure AD et Profil utilisateur SharePoint Online.

Dans le cadre de cet article, on part de l'hypothèse qu'une propriété utilisateur **Trigramme** est déjà présente dans **Azure Active Directory**.
Cette propriété est une chaine de 3 caractères reprenant les initiales de l'utilisateur.
Elle sera créée à l'identique côté Profil utilisateur dans SharePoint Online.
Une synchronisation entre les deux systèmes sera réalisée via **PnP PowerShell**

## Préambule

Notez que certaines propriétés sont déjà synchronisées par défaut. Une liste de ces propriétés peut être trouvée ici : https://learn.microsoft.com/sharepoint/user-profile-sync#properties-that-are-synced-into-sharepoint-user-profiles

Pour les autres propriétés qui ne sont pas listées sur cette page, vous pouvez utiliser les commandes décrits dans cet article pour les synchroniser.

## Azure Active Directory

## Profil utilisateur SharePoint Online

L'étape suivante est de créer dans Profil utilisateur SharePoint Online les propriétés équivalentes à celles disponibles dans Azure AD.

Pour plus de détails sur cette étape, vous pouvez consulter notre article précédent intitulé "Guide pas-à-pas pour ajouter une nouvelle propriété personnalisée dans le Profil Utilisateur SharePoint Online".

Dans la suite de cet article, nous partons du principe que la propriété personnalisée **Trigramme** est déjà disponible dans le **Profil utilisateur SharePoint Online**.

## Installation des modules AzureAD et PnP PowerShell

La première étape consiste à installer les modules AzureAD et PnP PowerShell sur votre machine. Ouvrez une fenêtre PowerShell en tant qu'administrateur et exécutez les commandes suivantes :

```
Install-Module AzureAD
Install-Module PnP.PowerShell -Scope CurrentUser
```

Cette commande téléchargera et installera la dernière version de ces modules à partir du PowerShell Gallery.

## Connexion à Azure AD et SharePoint Online

Après l'installation des modules AzureAD et PnP PowerShell, vous devez vous connecter à la fois à Azure AD et à SharePoint Online. Utilisez les commandes suivantes pour vous connecter :

```
Connect-AzureAD
Connect-PnPOnline -Url <URL-du-site-SharePoint> -UseWebLogin
```

La première commande vous permettra de vous connecter à Azure AD en utilisant les informations d'identification appropriées. La deuxième commande vous permettra de vous connecter à SharePoint Online en spécifiant l'URL du site SharePoint et en utilisant l'authentification basée sur le navigateur.

## Récupération des utilisateurs et de leurs propriétés dans Azure AD

Maintenant que vous êtes connecté, vous pouvez récupérer les utilisateurs et leurs propriétés dans Azure AD. Utilisez la commande suivante pour récupérer tous les utilisateurs :

```
$users = Get-AzureADUser -All $true
```

Cette commande stockera tous les utilisateurs dans la variable `$users`.

## Mise à jour des propriétés utilisateur dans SharePoint Online

```
foreach ($user in $users) {
    Set-PnPUserProfileProperty -Account $user.UserPrincipalName -PropertyName "Trigramme" -PropertyValue $user.EmployeeID
}
```

Cette boucle parcourt chaque utilisateur, utilise la commande `Set-PnPUserProfileProperty` pour mettre à jour la propriété **Trigramme** dans SharePoint Online en utilisant la valeur correspondante de la propriété **Trigramme** dans Azure AD.

## Vérification de la synchronisation des propriétés utilisateur

Une fois la synchronisation effectuée, vous pouvez vérifier si les propriétés utilisateur sont correctement mises à jour dans SharePoint Online. Utilisez la commande suivante pour récupérer les profils utilisateur :

```
$profiles = Get-PnPUserProfile
```

Cette commande stockera les profils utilisateur dans la variable `$profiles`. Vous pouvez ensuite afficher les propriétés mises à jour pour chaque utilisateur.

## Déconnexion de Azure AD et PnP PowerShell

Après avoir terminé toutes vos opérations, vous devez vous déconnecter à la fois de Azure AD et de SharePoint Online. Utilisez les commandes suivantes pour vous déconnecter :

```
Disconnect-PnPOnline
Disconnect-AzureAD
```

## Script complet de synchronisation

```
# Connect to Azure AD
Connect-AzureAD

# Connect to SharePoint Online
Connect-PnPOnline -Url <URL-du-site-SharePoint> -UseWebLogin

# Get all users from Azure AD
$users = Get-AzureADUser -All $true

# Loop through each user
foreach ($user in $users) {
    Set-PnPUserProfileProperty -Account $user.UserPrincipalName -PropertyName "Trigramme" -PropertyValue $user.EmployeeID
}

# Disconnect from SharePoint Online
Disconnect-PnPOnline

# Disconnect from Azure AD
Disconnect-AzureAD
```

## Conclusion

La synchronisation des propriétés utilisateur entre Microsoft Azure Active Directory et Profil utilisateur SharePoint Online est simplifiée grâce à l'utilisation de PnP PowerShell. En suivant les étapes décrites dans cet article, vous serez en mesure d'automatiser la synchronisation des propriétés utilisateur et de maintenir les informations à jour entre Azure AD et SharePoint Online. Cela facilitera la gestion centralisée des utilisateurs et permettra une utilisation plus efficace de ces services.
