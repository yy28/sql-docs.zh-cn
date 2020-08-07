---
title: 创建程序集 |Microsoft Docs
description: 使用 CREATE ASSEMBLY 在 SQL Server 中注册程序集，并指定其安全设置。 注册程序集以使用其功能。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 40ad7c3d165b0869f3cba9e6f703cd9e33ef199f
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948175"
---
# <a name="creating-an-assembly"></a>创建程序集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  托管数据库对象（如存储过程或触发器）先经过编译，然后部署到称为程序集的单元中。 托管 DLL 程序集必须在中注册， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 然后才能使用程序集提供的功能。 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中注册程序集，请使用 CREATE ASSEMBLY 语句。 本主题讨论如何使用 CREATE ASSEMBLY 语句在数据库中注册程序集，以及如何为程序集指定安全设置。  
  
## <a name="the-create-assembly-statement"></a>CREATE ASSEMBLY 语句  
 CREATE ASSEMBLY 语句用于在数据库中创建程序集。 以下是示例：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 FROM 子句指定要创建的程序集的路径名。 此路径既可以是通用命名约定 (UNC) 路径，也可以是计算机本地的物理文件路径。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不允许使用相同的名称、区域性和公钥来注册程序集的不同版本。  
  
 可以创建引用其他程序集的程序集。 当在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中创建程序集时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还将创建由根级别程序集引用的程序集（如果尚未在数据库中创建被引用程序集）。  
  
 将向数据库用户或用户角色授予在数据库中创建进而拥有程序集的权限。 为了创建程序集，数据库用户或角色应具有 CREATE ASSEMBLY 权限。  
  
 仅当满足以下条件时，程序集才能成功地引用其他程序集：  
  
-   所调用或被引用的程序集由同一个用户或角色所有。  
  
-   所调用或被引用的程序集是在同一个数据库中创建的。  
  
## <a name="specifying-security-when-creating-assemblies"></a>创建程序集时指定安全性  
 在数据库中创建程序集时 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，可以指定三个不同的安全级别之一，你的代码可以在其中运行： **SAFE**、 **EXTERNAL_ACCESS**或**UNSAFE**。 当运行**CREATE ASSEMBLY**语句时，将对代码程序集执行某些检查，这可能会导致程序集无法在服务器上注册。 有关详细信息，请参阅[CodePlex](https://msftengprodsamples.codeplex.com/)上的模拟示例。  
  
 **SAFE**是默认权限集，适用于大多数方案。 若要指定给定的安全级别，您可以按如下所示修改 CREATE ASSEMBLY 语句的语法：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 通过只需省略上述第三行代码，也可以通过**安全**权限集创建程序集：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 当程序集中的代码在**安全**权限集下运行时，它只能通过进程内托管提供程序在服务器中执行计算和数据访问。  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>创建 EXTERNAL_ACCESS 和 UNSAFE 程序集  
 **EXTERNAL_ACCESS**解决了代码需要访问服务器外部资源（如文件、网络、注册表和环境变量）的情况。 只要服务器访问外部资源，它就会模拟调用托管代码的用户的安全上下文。  
  
 不**安全**代码权限适用于程序集不安全或需要对受限制资源（如 Win32 API）的其他访问权限的情况 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
 若要在中创建**EXTERNAL_ACCESS**或**UNSAFE**程序集 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，必须满足以下两个条件之一：  
  
1.  程序集经过了强名称签名或使用证书进行了 Authenticode 签名。 此强名称 (或证书) 在中创建 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 为非对称密钥 (或证书) ，并且具有具有**外部访问**程序集权限的相应登录名 (或不安全程序集) 的不**安全程序**集权限 (。  
  
2.  数据库所有者 (DBO) 具有外部**访问**程序集的**外部访问 (程序集**) **或不**安全程序**集的**外部访问程序集或不安全程序集 (权限，并且数据库的[可信数据库属性](../../../relational-databases/security/trustworthy-database-property.md)设置为**ON**。  

 在加载程序集（包括执行）时，也将检查上面所列的两个条件。 至少必须满足这些条件之一才能加载程序集。  
  
 建议不要将数据库上的 "[可信数据库" 属性](../../../relational-databases/security/trustworthy-database-property.md)设置为 **"仅在**服务器进程中运行公共语言运行时 (CLR) 代码。 而是建议在 master 数据库中通过程序集文件创建非对称密钥。 然后，必须创建映射到此非对称密钥的登录名，并且必须向该登录名授予**EXTERNAL ACCESS assembly**或**UNSAFE ASSEMBLY**权限。  
  
 以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句执行创建非对称密钥所需的步骤，将登录名映射到此密钥，然后将**EXTERNAL_ACCESS**权限授予该登录名。 必须运行以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，然后才能运行 CREATE ASSEMBLY 语句。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  必须创建新的登录名以与非对称密钥关联。 此登录名仅用于授予权限；不必与用户关联或在应用程序中使用。  
  
 若要创建**外部访问**程序集，创建者需要具有**外部访问**权限。 此权限在创建程序集时指定：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句执行创建非对称密钥所需的步骤，将登录名映射到此密钥，然后将**UNSAFE**权限授予该登录名。 必须运行以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，然后才能运行 CREATE ASSEMBLY 语句。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 若要指定使用**UNSAFE**权限加载程序集，请在将程序集加载到服务器时指定**unsafe**权限集：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 有关每个设置的权限的详细信息，请参阅[CLR 集成安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [管理 CLR 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [更改程序集](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [删除程序集](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY 数据库属性](../../../relational-databases/security/trustworthy-database-property.md)