---
title: 使用 Azure Active Directory |SQL Server 的 Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 44f92e782a497005ea47847301279e4341722d36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68213557"
---
# <a name="using-azure-active-directory"></a>使用 Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>用途

从版本18.2.1 开始, 适用于 SQL Server 的 Microsoft OLE DB 驱动程序允许 OLE DB 应用程序使用联合身份连接到 Azure SQL 数据库的实例。 新的身份验证方法包括:
- Azure Active Directory 登录 ID 和密码
- Azure Active Directory 访问令牌
- Azure Active Directory 集成身份验证
- SQL 登录 ID 和密码

> [!NOTE]  
> 将以下 Azure Active Directory 选项与 OLE DB 驱动程序一起使用时, 请确保已安装[SQL Server Active Directory 身份验证库](https://go.microsoft.com/fwlink/?LinkID=513072):
> - Azure Active Directory 登录 ID 和密码
> - Azure Active Directory 集成身份验证
>
> 其他身份验证方法或 OLE DB 操作不需要 ADAL。

> [!NOTE]
> 不支持将下列身份验证`DataTypeCompatibility`模式 (或其对应的属性) `80`设置  为:
> - 使用登录 ID 和密码 Azure Active Directory 身份验证
> - 使用访问令牌进行 Azure Active Directory 身份验证
> - Azure Active Directory 集成身份验证

## <a name="connection-string-keywords-and-properties"></a>连接字符串关键字和属性
引入了以下连接字符串关键字, 以支持 Azure Active Directory 身份验证:

|连接字符串关键字|连接属性|描述|
|---               |---                |---        |
|访问令牌|SSPROP_AUTH_ACCESS_TOKEN|指定对 Azure Active Directory 进行身份验证的访问令牌。 |
|身份验证|SSPROP_AUTH_MODE|指定要使用的身份验证方法。|

有关新关键字/属性的详细信息, 请参阅以下页面:
- [将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初始化和授权属性](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>加密和证书验证
本部分讨论加密和证书验证行为的更改。 仅当使用新的身份验证或访问令牌连接字符串关键字 (或其对应的属性) 时, 这些更改**才**有效。

### <a name="encryption"></a>加密
为了提高安全性, 当使用新的连接属性/关键字时, 驱动程序会通过将其设置为来`yes`覆盖默认的加密值。 重写在数据源对象初始化时发生。 如果在通过任何方法初始化之前设置加密, 则会考虑该值, 而不会重写该值。

> [!NOTE]   
> 在 ADO 应用程序以及通过`IDBInitialize` `IDataInitialize::GetDataSource`获取接口的应用程序中, 实现接口的核心组件会将加密显式设置`no`为其默认值。 因此, 新的身份验证属性/关键字遵循此设置, 并且**不**会重写加密值。 因此,**建议**将这些应用程序显式设置`Use Encryption for Data=true`为替代默认值。

### <a name="certificate-validation"></a>证书验证
为了提高安全性, 新的连接属性/关键字`TrustServerCertificate`与**客户端加密设置无关**, 而不是与客户端加密设置相同。 因此, 默认情况下会验证服务器证书。

> [!NOTE]   
> 还可以通过`Value` `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`注册表条目的字段控制证书验证。 有效值为 `0` 或 `1`。 OLE DB 驱动程序在注册表和连接属性/关键字设置之间选择最安全的选项。 也就是说, 只要至少有一个注册表/连接设置启用服务器证书验证, 驱动程序就会验证服务器证书。

## <a name="gui-additions"></a>GUI 添加
驱动程序图形用户界面已增强为允许 Azure Active Directory 身份验证。 有关详细信息，请参阅：
- [SQL Server 登录对话框](../help-topics/sql-server-login-dialog.md)
- [通用数据链接 (UDL) 配置](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>连接字符串示例
此部分显示与`IDataInitialize::GetDataSource`和`DBPROP_INIT_PROVIDERSTRING`属性一起使用的新的和现有的连接字符串关键字的示例。

### <a name="sql-authentication"></a>SQL 身份验证
- 使用 `IDataInitialize::GetDataSource`：
    - 新建:
        > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];**Authentication = SqlPassword**;User ID = [username];Password = [password];对 Data 使用 Encryption = true
    - 不推荐使用：
        > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];User ID = [username];Password = [password];对 Data 使用 Encryption = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新建:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 不推荐使用：
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>使用安全支持提供程序接口 (SSPI) 的集成 Windows 身份验证

- 使用 `IDataInitialize::GetDataSource`：
    - 新建:
        > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];**Authentication = ActiveDirectoryIntegrated**;对 Data 使用 Encryption = true
    - 不推荐使用：
        > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];**集成安全性 = SSPI**;对 Data 使用 Encryption = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新建:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 不推荐使用：
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="aad-username-and-password-authentication-using-adal"></a>使用 ADAL 进行 AAD 用户名和密码身份验证

- 使用 `IDataInitialize::GetDataSource`：
    > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];**Authentication = ActiveDirectoryPassword**;User ID = [username];Password = [password];对 Data 使用 Encryption = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>使用 ADAL 进行集成的 Azure Active Directory 身份验证

- 使用 `IDataInitialize::GetDataSource`：
    > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];**Authentication = ActiveDirectoryIntegrated**;对 Data 使用 Encryption = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>使用访问令牌 Azure Active Directory 身份验证

- 使用 `IDataInitialize::GetDataSource`：
    > Provider = MSOLEDBSQL; Data Source = [server]; 初始目录 = [数据库];**访问令牌 = [访问令牌]** ;对 Data 使用 Encryption = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > 不支持通过`DBPROP_INIT_PROVIDERSTRING`提供访问令牌

## <a name="code-samples"></a>代码示例

以下示例显示了连接到 Azure Active Directory 与连接关键字所需的代码。 

### <a name="access-token"></a>访问令牌
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Active Directory 已集成
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>后续步骤
- [使用 OAuth 2.0 代码授予流授予对 Azure Active Directory web 应用程序的访问权限](https://go.microsoft.com/fwlink/?linkid=2072672)。

- 了解 SQL Server 的 [Azure Active Directory 身份验证](https://go.microsoft.com/fwlink/?linkid=2073783)。

- 使用 OLE DB 驱动程序支持的[连接字符串关键字](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)配置驱动程序连接。
