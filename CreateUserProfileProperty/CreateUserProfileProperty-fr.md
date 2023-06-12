# Guide étape par étape pour ajouter une nouvelle propriété personnalisée dans le Profil Utilisateur de SharePoint Online

Dans SharePoint Online, le Profil Utilisateur joue un rôle clé pour stocker et gérer les informations relatives aux utilisateurs. Bien que SharePoint Online offre un ensemble de propriétés prédéfinies, il est parfois nécessaire d'ajouter des propriétés personnalisées pour répondre aux besoins spécifiques de votre organisation. Dans cet article, nous allons vous guider à travers les étapes pour ajouter une nouvelle propriété personnalisée dans le Profil Utilisateur de SharePoint Online. Dans le cadre de cet article, nous allons créer une nouvelle propriété utilisateur Trigramme qui est une chaine de 3 caractères reprenant les initiales de l'utilisateur.

## Accéder au Centre d'administration SharePoint Online

Pour commencer, connectez-vous au Centre d'administration SharePoint Online à l'aide d'un compte disposant des droits d'administration.
L'URL du Centre d'administration SharePoint Online est https://{tenant}-admin.sharepoint.com en remplaçant {tenant} par le nom de votre tenant.

![Image](SharePointCentralAdmin.png)

## Accéder aux Paramètres du Profil Utilisateur

Dans le Centre d'administration SharePoint Online, cliquez sur "Plus de fonctionnalités" dans le menu de gauche, puis sélectionnez "Profils utilisateur".

![Image](MoreFeatures.png)

## Créer une nouvelle propriété personnalisée

Dans la page "Profils utilisateur", cliquez sur "Gérer les propriétés utilisateur" pour afficher la liste des propriétés existantes.

![Image](UserProfileHome.png)

## Remplir les détails de la propriété

Dans le formulaire de création, remplissez les informations suivantes :

- Nom : Entrez un nom significatif pour votre propriété personnalisée.
- Type de données : Sélectionnez le type de données approprié pour votre propriété (texte, nombre, date/heure, etc.)
- Longueur maximale : Définissez la longueur maximale de la valeur de propriété.

Dans le cadre de cet article, nous créons une nouvelle propriété utilisateur Trigramme qui est une chaine de 3 caractères reprenant les initiales de l'utilisateur.

![Image](NewPropertyForm1.png)

Dans les Paramètres de recherche, pensez à cocher la case Indexé si vous souhaitez que cette propriété apparaisse dans les résultats de recherche.

![Image](NewPropertyForm2.png)

A noter que la synchronisation des données avec les propriétés Azure Active Directory n'est pas possible ici et il faudra donc le faire après coup via un script PowerShell.

## Enregistrer la propriété

Une fois que vous avez rempli tous les détails de la propriété, cliquez sur le bouton "OK" pour l'enregistrer.

![Image](NewPropertyForm3.png)

## Synchroniser les propriétés

Après avoir ajouté une nouvelle propriété personnalisée, vous devez vous assurer que les profils utilisateurs sont synchronisés avec Active Directory. Comme mentionné précédemment, la synchronisation avec Azure Active Directory doit être réalisée via un script PowerShell. Plus d'informations disponibles sur cette partie ici : https://learn.microsoft.com/en-us/sharepoint/user-profile-sync
Cette étape spécifique fera l'objet d'un prochain article.

## Conclusion

En suivant les étapes décrites ci-dessus, vous pouvez facilement ajouter une propriété personnalisée au Profil Utilisateur de SharePoint Online et la configurer pour qu'elle remonte dans les résultats de recherche. Cette fonctionnalité offre une meilleure recherche et une utilisation plus efficace des informations utilisateur dans votre environnement SharePoint Online. N'oubliez pas de synchroniser les profils utilisateurs avec Azure Active Directory et de configurer l'indexation appropriée pour que la propriété personnalisée soit pleinement fonctionnelle. Profitez de cette personnalisation pour améliorer la pertinence des résultats de recherche dans votre organisation.
