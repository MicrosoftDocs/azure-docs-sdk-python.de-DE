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
ms.openlocfilehash: 4cf4149dfbd8209020e3affc0d15ab870f8d9697
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276744"
---
# <a name="azure-active-directory-libraries-for-python"></a>Azure Active Directory-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Mit [Azure Active Directory](/azure/active-directory/active-directory-whatis) können Sie Benutzer anmelden und den Zugriff auf Anwendungen und APIs steuern.

## <a name="client-library"></a>Clientbibliothek

Konfigurieren Sie OAuth2-, OpenID Connect- oder Active Directory Graph-Authentifizierung und [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)-SSO mit der [Azure Active Directory-Authentifizierungsbibliothek (ADAL) für Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).

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

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/python/api/overview/azure/activedirectory/client)

Sehen Sie sich weitere [Python-Codebeispiele für Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) an, die Sie in Ihren Apps verwenden können.
