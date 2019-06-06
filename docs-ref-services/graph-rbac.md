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
# <a name="azure-active-directory-graph-libraries-for-python"></a><span data-ttu-id="594bb-104">Azure Active Directory Graph-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="594bb-104">Azure Active Directory Graph libraries for Python</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="594bb-105">Im Februar 2019 haben wir begonnen, einige frühere Versionen der Azure Active Directory Graph-API zugunsten der Microsoft Graph-API als veraltet zu markieren.</span><span class="sxs-lookup"><span data-stu-id="594bb-105">As of February 2019, we started the process to deprecate some earlier versions of Azure Active Directory Graph API in favor of the Microsoft Graph API.</span></span> 
>
> <span data-ttu-id="594bb-106">Detaillierte Informationen, Updates und den Zeitrahmen finden Sie im Office Dev Center unter [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) (Microsoft Graph oder Azure AD Graph).</span><span class="sxs-lookup"><span data-stu-id="594bb-106">For details, updates, and time frames, see [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) in the Office Dev Center.</span></span>
>
> <span data-ttu-id="594bb-107">In Zukunft sollten Anwendungen die Microsoft Graph-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="594bb-107">Moving forward, applications should use the Microsoft Graph API.</span></span> 

## <a name="overview"></a><span data-ttu-id="594bb-108">Übersicht</span><span class="sxs-lookup"><span data-stu-id="594bb-108">Overview</span></span> 

<span data-ttu-id="594bb-109">Mit [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-apis) können Sie Benutzer anmelden und den Zugriff auf Anwendungen und APIs steuern.</span><span class="sxs-lookup"><span data-stu-id="594bb-109">Sign-on users and control access to applications and APIs with [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-apis).</span></span>   

## <a name="client-library"></a><span data-ttu-id="594bb-110">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="594bb-110">Client library</span></span>   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a><span data-ttu-id="594bb-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="594bb-111">Example</span></span> 
> [!NOTE]   
> <span data-ttu-id="594bb-112">Beim Erstellen der Instanz für die Anmeldeinformationen muss der Ressourcenparameter in https://graph.windows.net geändert werden.</span><span class="sxs-lookup"><span data-stu-id="594bb-112">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>    
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
<span data-ttu-id="594bb-113">Mit dem folgenden Code wird ein Benutzer erstellt, direkt und mittels Listenfilterung abgerufen und dann gelöscht.</span><span class="sxs-lookup"><span data-stu-id="594bb-113">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>   
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