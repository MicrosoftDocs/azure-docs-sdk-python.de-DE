---
title: Graph RBAC-Bibliotheken für Python
description: Referenz zu Graph RBAC-Bibliotheken für Python
keywords: Azure, Python, SDK, API, Graph RBAC
author: rloutlaw
ms.author: routlaw
manager: jfriend
ms.date: 05/10/2019
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 27238e00463ae30ec0e47e8c18497ffb9edac62c
ms.sourcegitcommit: 253c8d4b3dbc2bb76d1a273a757ab96ba37617a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2019
ms.locfileid: "65731536"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a>Azure Active Directory Graph-Bibliotheken für Python

> [!IMPORTANT]
>
> Im Februar 2019 haben wir begonnen, einige frühere Versionen der Azure Active Directory Graph-API zugunsten der Microsoft Graph-API als veraltet zu markieren. 
>
> Detaillierte Informationen, Updates und den Zeitrahmen finden Sie im Office Dev Center unter [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) (Microsoft Graph oder Azure AD Graph).
>
> In Zukunft sollten Anwendungen die Microsoft Graph-API verwenden. 

## <a name="overview"></a>Übersicht 

Mit [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-apis) können Sie Benutzer anmelden und den Zugriff auf Anwendungen und APIs steuern.   

## <a name="client-library"></a>Clientbibliothek   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a>Beispiel 
> [!NOTE]   
> Beim Erstellen der Instanz für die Anmeldeinformationen muss der Ressourcenparameter in https://graph.windows.net geändert werden.    
 ```python  
from azure.graphrbac import GraphRbacManagementClient   
from azure.common.credentials import UserPassCredentials    
 credentials = UserPassCredentials( 
            'user@domain.com',      # Your user 
            'my_password',          # Your password 
            resource="https://graph.windows.net"    
    )   
 tenant_id = "myad.onmicrosoft.com" 
 graphrbac_client = GraphRbacManagementClient(  
    credentials,    
    tenant_id   
)   
``` 
Mit dem folgenden Code wird ein Benutzer erstellt, direkt und mittels Listenfilterung abgerufen und dann gelöscht.   
```python   
from azure.graphrbac.models import UserCreateParameters, PasswordProfile    
 user = graphrbac_client.users.create(  
    UserCreateParameters(   
        user_principal_name="testbuddy@{}".format(MY_AD_DOMAIN),    
        account_enabled=False,  
        display_name='Test Buddy',  
        mail_nickname='testbuddy',  
        password_profile=PasswordProfile(   
            password='MyStr0ngP4ssword',    
            force_change_password_next_login=True   
        )   
    )   
)   
# user is a User instance   
self.assertEqual(user.display_name, 'Test Buddy')   
 user = graphrbac_client.users.get(user.object_id)  
self.assertEqual(user.display_name, 'Test Buddy')   
 for user in graphrbac_client.users.list(filter="displayName eq 'Test Buddy'"): 
    self.assertEqual(user.display_name, 'Test Buddy')   
 graphrbac_client.users.delete(user.object_id)  
```