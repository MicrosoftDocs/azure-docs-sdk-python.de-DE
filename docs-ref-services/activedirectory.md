---
title: Azure Active Directory-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken für Azure Active Directory
keywords: Azure, Python, SDK, API, SQL, Authentifizierung, AAD, Active Directory, Graph, OAuth 2.0
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: active-directory
ms.openlocfilehash: 78df70001dd0d55ac2c9c9da04fac6a51c5919e6
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478923"
---
# <a name="azure-active-directory-libraries-for-python"></a><span data-ttu-id="dbc80-104">Azure Active Directory-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="dbc80-104">Azure Active Directory libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="dbc80-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="dbc80-105">Overview</span></span>

<span data-ttu-id="dbc80-106">Mit [Azure Active Directory](/azure/active-directory/active-directory-whatis) können Sie Benutzer anmelden und den Zugriff auf Anwendungen und APIs steuern.</span><span class="sxs-lookup"><span data-stu-id="dbc80-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

## <a name="client-library"></a><span data-ttu-id="dbc80-107">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="dbc80-107">Client library</span></span>

<span data-ttu-id="dbc80-108">Konfigurieren Sie OAuth2-, OpenID Connect- oder Active Directory Graph-Authentifizierung und [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)-SSO mit der [Azure Active Directory-Authentifizierungsbibliothek (ADAL) für Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).</span><span class="sxs-lookup"><span data-stu-id="dbc80-108">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).</span></span>

```bash
pip install azure-graphrbac
```

### <a name="example"></a><span data-ttu-id="dbc80-109">Beispiel</span><span class="sxs-lookup"><span data-stu-id="dbc80-109">Example</span></span>
> [!NOTE]
> <span data-ttu-id="dbc80-110">Beim Erstellen der Instanz für die Anmeldeinformationen muss der Ressourcenparameter in „https://graph.windows.net“ geändert werden.</span><span class="sxs-lookup"><span data-stu-id="dbc80-110">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>

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
<span data-ttu-id="dbc80-111">Mit dem folgenden Code wird ein Benutzer erstellt, direkt und mittels Listenfilterung abgerufen und dann gelöscht.</span><span class="sxs-lookup"><span data-stu-id="dbc80-111">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>
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

> [!div class="nextstepaction"]
> [<span data-ttu-id="dbc80-112">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="dbc80-112">Explore the Client APIs</span></span>](/python/api/overview/azure/activedirectory/client)

<span data-ttu-id="dbc80-113">Sehen Sie sich weitere [Python-Codebeispiele für Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) an, die Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="dbc80-113">Explore more [sample Python code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) you can use in your apps.</span></span>