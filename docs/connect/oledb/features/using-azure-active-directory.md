---
title: 使用 Azure Active Directory |适用于 SQL Server 的 Microsoft 文档
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
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744800"
---
# <a name="using-azure-active-directory"></a>使用 Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>用途

从版本 18.2.1 开始，Microsoft OLE DB 驱动程序适用于 SQL Server 允许 OLE DB 应用程序连接到 Azure SQL 数据库实例使用联合的标识。 新的身份验证方法包括：
- Azure Active Directory 登录 ID 和密码
- Azure Active Directory 访问令牌
- Azure Active Directory 集成身份验证
- SQL 登录 ID 和密码

> [!NOTE]  
> 当通过 OLE DB 驱动程序使用以下 Azure Active Directory 选项，确保[SQL Server 的 Active Directory 身份验证库](https://go.microsoft.com/fwlink/?LinkID=513072)已安装：
> - Azure Active Directory 登录 ID 和密码
> - Azure Active Directory 集成身份验证
>
> ADAL 不需要其他身份验证方法或 OLE DB 操作。

> [!NOTE]
> 使用与以下身份验证模式`DataTypeCompatibility`（或其相应的属性） 设置为`80`是**不**支持：
> - 使用登录 ID 和密码的 azure Active Directory 身份验证
> - 使用访问令牌的 azure Active Directory 身份验证
> - Azure Active Directory 集成身份验证

## <a name="connection-string-keywords-and-properties"></a>连接字符串关键字和属性
引入了以下连接字符串关键字，以支持 Azure Active Directory 身份验证：

|连接字符串关键字|连接属性|描述|
|---               |---                |---        |
|访问令牌|SSPROP_AUTH_ACCESS_TOKEN|指定要向 Azure Active Directory 进行身份验证的访问令牌。 |
|身份验证|SSPROP_AUTH_MODE|指定要使用的身份验证方法。|

新的关键字/属性的详细信息，请参阅以下页面：
- [将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初始化和授权属性](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>加密和证书验证
本部分讨论中加密和证书验证行为的更改。 这些更改是**仅**生效时使用新的身份验证或访问令牌连接字符串关键字 （或其对应的属性）。

### <a name="encryption"></a>加密
若要提高安全性，使用新连接属性/关键字时，该驱动程序将覆盖默认加密值设置为`yes`。 重写发生在数据源对象初始化时。 如果通过任何方式在初始化之前设置加密，值是考虑，不重写。

> [!NOTE]   
> ADO 应用程序在和中获取的应用程序`IDBInitialize`通过接口`IDataInitialize::GetDataSource`，显式实现接口的核心组件将加密设置为其默认值为`no`。 因此，新身份验证属性/关键字遵循此设置和加密值**不是**重写。 因此，很**建议**这些应用程序显式设置`Use Encryption for Data=true`来覆盖默认值。

### <a name="certificate-validation"></a>证书验证
为了提高安全性，新连接属性/关键字尊重`TrustServerCertificate`设置 （和其相应的连接字符串关键字/属性）**独立于客户端加密设置**。 因此，默认情况下验证服务器证书。

> [!NOTE]   
> 此外可以通过控制证书验证`Value`字段的`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`注册表项。 有效值为 `0` 或 `1`。 OLE DB 驱动程序选择注册表和连接属性/关键字设置之间的最安全选项。 也就是说，该驱动程序将验证服务器证书，只要在至少一个注册表/连接设置启用服务器证书验证。

## <a name="gui-additions"></a>GUI 新增功能
驱动程序图形用户界面已得到增强，以允许 Azure Active Directory 身份验证。 有关详细信息，请参阅：
- [SQL Server 登录对话框](../help-topics/sql-server-login-dialog.md)
- [通用数据链接 (UDL) 配置](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>连接字符串示例
本部分显示了示例的新的和现有的连接字符串关键字以用于`IDataInitialize::GetDataSource`和`DBPROP_INIT_PROVIDERSTRING`属性。

### <a name="sql-authentication"></a>SQL 身份验证
- 使用 `IDataInitialize::GetDataSource`：
    - 新建:
        > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];**身份验证 = SqlPassword**;用户 ID = [username];密码 = [password];使用数据加密 = true
    - 不推荐使用：
        > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];用户 ID = [username];密码 = [password];使用数据加密 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新建:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 不推荐使用：
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>使用安全支持提供程序接口 (SSPI) 进行集成的 Windows 身份验证

- 使用 `IDataInitialize::GetDataSource`：
    - 新建:
        > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];**身份验证 = ActiveDirectoryIntegrated**;使用数据加密 = true
    - 不推荐使用：
        > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];**集成安全性 = SSPI**;使用数据加密 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    - 新建:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 不推荐使用：
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="aad-username-and-password-authentication-using-adal"></a>AAD 用户名和密码身份验证使用 ADAL

- 使用 `IDataInitialize::GetDataSource`：
    > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];**身份验证 = ActiveDirectoryPassword**;用户 ID = [username];密码 = [password];使用数据加密 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>使用 ADAL 的集成的 Azure Active Directory 身份验证

- 使用 `IDataInitialize::GetDataSource`：
    > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];**身份验证 = ActiveDirectoryIntegrated**;使用数据加密 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>使用访问令牌的 azure Active Directory 身份验证

- 使用 `IDataInitialize::GetDataSource`：
    > 提供程序 = MSOLEDBSQL; 数据源 = [服务器]; Initial Catalog = [数据库];**访问令牌 = [访问令牌]**;使用数据加密 = true
- 使用 `DBPROP_INIT_PROVIDERSTRING`：
    > 提供访问令牌通过`DBPROP_INIT_PROVIDERSTRING`不受支持

## <a name="code-samples"></a>代码示例

下面的示例演示所需连接到 Azure Active Directory 与连接关键字的代码。 

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
- [授权访问 Azure Active Directory web 应用程序使用 OAuth 2.0 代码授予流](https://go.microsoft.com/fwlink/?linkid=2072672)。

- 了解 SQL Server 的 [Azure Active Directory 身份验证](https://go.microsoft.com/fwlink/?linkid=2073783)。

- 配置使用的驱动程序连接[连接字符串关键字](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)OLE DB 驱动程序支持。
