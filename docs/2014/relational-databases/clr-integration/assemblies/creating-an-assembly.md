---
title: 创建程序集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: e28871e93bd718063692a31a4a3462399517dfc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919576"
---
# <a name="creating-an-assembly"></a>创建程序集
  托管数据库对象（如存储过程或触发器）先经过编译，然后部署到称为程序集的单元中。 托管的 DLL 程序集必须在注册[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]才能使用该程序集提供的功能。 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中注册程序集，请使用 CREATE ASSEMBLY 语句。 本主题讨论如何使用 CREATE ASSEMBLY 语句在数据库中注册程序集，以及如何为程序集指定安全设置。  
  
## <a name="the-create-assembly-statement"></a>CREATE ASSEMBLY 语句  
 CREATE ASSEMBLY 语句用于在数据库中创建程序集。 以下是示例：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 FROM 子句指定要创建的程序集的路径名。 此路径既可以是通用命名约定 (UNC) 路径，也可以是计算机本地的物理文件路径。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不允许使用相同的名称、区域性和公钥来注册程序集的不同版本。  
  
 可以创建引用其他程序集的程序集。 在创建程序集时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]还会创建由根级别程序集引用的程序集如果引用的程序集是否尚未创建到数据库。  
  
 将向数据库用户或用户角色授予在数据库中创建进而拥有程序集的权限。 为了创建程序集，数据库用户或角色应具有 CREATE ASSEMBLY 权限。  
  
 仅当满足以下条件时，程序集才能成功地引用其他程序集：  
  
-   所调用或被引用的程序集由同一个用户或角色所有。  
  
-   所调用或被引用的程序集是在同一个数据库中创建的。  
  
## <a name="specifying-security-when-creating-assemblies"></a>创建程序集时指定安全性  
 当在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中创建程序集时，可以指定您的代码可在以下三种安全级别的哪一种下运行：`SAFE`、`EXTERNAL_ACCESS` 或 `UNSAFE`。 当运行 `CREATE ASSEMBLY` 语句时，会对代码程序集执行某些检查，看看是否存在可能导致程序集无法在服务器上注册的问题。 有关详细信息，请参阅 》 上模拟示例[CodePlex](http://msftengprodsamples.codeplex.com/)。  
  
 `SAFE` 是默认的权限集，适用于绝大多数应用场景。 若要指定给定的安全级别，您可以按如下所示修改 CREATE ASSEMBLY 语句的语法：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 也可以通过只是省略上述代码的第三行，使用 `SAFE` 权限集创建程序集：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 当程序集中的代码在 `SAFE` 权限集下运行时，它只能通过进程中的托管提供程序在服务器内执行计算和数据访问。  
  
### <a name="creating-externalaccess-and-unsafe-assemblies"></a>创建 EXTERNAL_ACCESS 和 UNSAFE 程序集  
 `EXTERNAL_ACCESS` 适用于代码需要访问服务器之外的资源（如文件、网络、注册表和环境变量）的应用场景。 只要服务器访问外部资源，它就会模拟调用托管代码的用户的安全上下文。  
  
 `UNSAFE` 代码权限适用的场合为：程序集并非可验证为安全的，或程序集要求进一步访问受限资源（如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 API）。  
  
 为了在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中创建 `EXTERNAL_ACCESS` 或 `UNSAFE` 程序集，必须满足以下两个条件：  
  
1.  程序集经过了强名称签名或使用证书进行了 Authenticode 签名。 此强名称（或证书）在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部作为非对称密钥（或证书）创建，它具有对应的带有 `EXTERNAL ACCESS ASSEMBLY` 权限（对于外部访问程序集）或 `UNSAFE ASSEMBLY` 权限（对于不安全的程序集）的登录名。  
  
2.  数据库所有者 (DBO) 拥有`EXTERNAL ACCESS ASSEMBLY`(对于`EXTERNAL ACCESS`程序集) 或`UNSAFE ASSEMBLY`(对于`UNSAFE`程序集) 的权限，并且数据库已[TRUSTWORTHY 数据库属性](../../security/trustworthy-database-property.md)设置为`ON`。  
  
 在加载程序集（包括执行）时，也将检查上面所列的两个条件。 至少必须满足这些条件之一才能加载程序集。  
  
 我们建议[TRUSTWORTHY 数据库属性](../../security/trustworthy-database-property.md)在数据库上不是设置为`ON`仅将运行公共语言运行时 (CLR) 代码，在服务器进程中。 而是建议在 master 数据库中通过程序集文件创建非对称密钥。 然后，必须创建映射到此非对称密钥的登录名，并且必须向此登录名授予 `EXTERNAL ACCESS ASSEMBLY` 或 `UNSAFE ASSEMBLY` 权限。  
  
 以下[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句，然后才能运行 CREATE ASSEMBLY 语句。  
  
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
  
 若要创建 `EXTERNAL ACCESS` 程序集，创建者需要具有 `EXTERNAL ACCESS` 权限。 此权限在创建程序集时指定：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 以下[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句，然后才能运行 CREATE ASSEMBLY 语句。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 若要指定使用 `UNSAFE` 权限加载程序集，则当将程序集加载到服务器时，应指定 `UNSAFE` 权限集。  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 有关每个设置的权限的更多详细信息，请参阅[CLR 集成安全性](../security/clr-integration-security.md)。  
  
## <a name="see-also"></a>请参阅  
 [管理 CLR 集成程序集](managing-clr-integration-assemblies.md)   
 [更改程序集](altering-an-assembly.md)   
 [删除程序集](dropping-an-assembly.md)   
 [CLR 集成代码访问安全性](../security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY 数据库属性](../../security/trustworthy-database-property.md)   
 [允许部分可信任的调用方](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
  
  
