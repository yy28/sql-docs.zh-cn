---
title: "创建程序集 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 8/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASSEMBLY
- CREATE ASSEMBLY
- CREATE_ASSEMBLY_TSQL
- ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], validating
- validating assemblies
- CREATE ASSEMBLY statement
- assemblies [CLR integration], creating
ms.assetid: d8d1d245-c2c3-4325-be52-4fc1122c2079
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f937dc219eb317347cceeafcdcd8753244bcb07
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-assembly-transact-sql"></a>CREATE ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建包含类元数据和托管代码的托管应用程序模块，将其作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的对象。 通过引用此模块，可在数据库中创建公共语言运行时 (CLR) 函数、存储过程、触发器、用户定义聚合以及用户定义类型。  
  
>  [!WARNING]
>  CLR 在 .NET Framework 中使用代码访问安全性 (CAS)（不可再作为安全边界）。 使用 `PERMISSION_SET = SAFE` 创建的 CLR 程序集可以访问外部系统资源、调用非托管代码以及获取 sysadmin 特权。 从 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 开始，引入了名为 `clr strict security` 的 `sp_configure` 选项，以增强 CLR 程序集的安全性。 默认启用 `clr strict security`，并将 `SAFE` 和 `EXTERNAL_ACCESS` 程序集与标记为 `UNSAFE` 的程序集同等对待。 可禁用 `clr strict security` 选项以实现后向兼容性，但不建议这样做。 Microsoft 建议所有程序集都通过证书或非对称密钥进行签名，且该证书或非对称密钥具有已在主数据库中获得 `UNSAFE ASSEMBLY` 权限的相应登录名。 有关详细信息，请参阅 [CLR 严格安全性](../../database-engine/configure-windows/clr-strict-security.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE ASSEMBLY assembly_name  
[ AUTHORIZATION owner_name ]  
FROM { <client_assembly_specifier> | <assembly_bits> [ ,...n ] }  
[ WITH PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE } ]  
[ ; ]  
<client_assembly_specifier> :: =  
        '[\\computer_name\]share_name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```  
  
## <a name="arguments"></a>参数  
 *assembly_name*  
 程序集的名称。 名称必须是唯一在数据库和有效[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 授权*owner_name*  
 指定作为程序集所有者的用户或角色的名称。 *owner_name*必须要么是的角色的当前用户是成员，或者当前用户必须具有 IMPERSONATE 权限的名称*owner_name*。 如果未指定，则所有权授予当前用户。  
  
 \<client_assembly_specifier>  
指定正在上载的程序集所在的本地路径或网络位置，以及与程序集对应的清单文件名。  \<client_assembly_specifier > 可以表示为一个固定的字符串或表达式评估结果为固定的字符串，使用变量。 CREATE ASSEMBLY 不支持加载多模块程序集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还将在同一位置查找此程序集的所有相关程序集，并使用与根级别程序集相同的所有者将其上载。 如果没有找到这些相关程序集且它们尚未加载到当前数据库中，则 CREATE ASSEMBLY 失败。 如果相关程序集已加载到当前数据库中，则这些程序集的所有者必须与新创建的程序集的所有者相同。
  
 \<client_assembly_specifier > 不能指定是否被模拟登录的用户。  
  
 \<assembly_bits>  
 组成程序集和依赖程序集的二进制值的列表。 列表中的第一个值将视为根级程序集。 与相关程序集对应的值可以按任意顺序提供。 所有与根程序集的依赖项不相对应的值都将忽略。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 *varbinary_literal*  
 是**varbinary**文本。  
  
 *varbinary_expression*  
 类型的表达式**varbinary**。  
  
 PERMISSION_SET {**安全**|EXTERNAL_ACCESS |不安全}  
 >  [!IMPORTANT]  
 >  `PERMISSION_SET`选项受`clr strict security`选项，打开警告中所述。 当`clr strict security`是启用，所有程序集被视为`UNSAFE`。
 
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问程序集时向程序集授予的一组代码访问权限。 如果未指定，则将 SAFE 用作默认值。  
  
 我们推荐使用 SAFE。 SAFE 是最具限制性的权限集。 由具有 SAFE 权限的程序集所执行的代码将无法访问外部系统资源，例如文件、网络、环境变量或注册表。  
  
 EXTERNAL_ACCESS 使程序集可以访问某些外部系统资源，例如文件、网络、环境变量以及注册表。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 UNSAFE 可使程序集不受限制地访问资源，无论是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例内部还是外部的资源都可以访问。 从 UNSAFE 程序集内运行的代码可调用未托管代码。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
> [!IMPORTANT]  
>  对于执行计算和数据管理任务而无需访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例外部资源的程序集，SAFE 是推荐的权限设置。  
>   
>  对于访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例外部资源的程序集，我们推荐使用 EXTERNAL_ACCESS。 EXTERNAL_ACCESS 程序集包含 SAFE 程序集的可靠性和可伸缩性保护，但从安全角度而言，它与 UNSAFE 程序集类似。 原因是在默认情况下，EXTERNAL_ACCESS 程序集中的代码以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户身份运行并访问此帐户的外部资源，除非此代码显式模拟调用方。 因此，创建 EXTERNAL_ACCESS 程序集的权限应只授予以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户身份运行代码的可信登录。 有关模拟的详细信息，请参阅[CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)。  
>   
>  指定 UNSAFE 将使程序集中的代码在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程空间中完全自由地执行操作，但这些操作可能危及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的可靠性。 UNSAFE 程序集也可能破坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或公共语言运行时的安全系统。 UNSAFE 权限只应授予高度可信的程序集。 只有的成员**sysadmin**固定的服务器角色可以创建和更改 UNSAFE 程序集。  
  
 有关程序集的权限集的详细信息，请参阅[设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
## <a name="remarks"></a>注释  
 CREATE ASSEMBLY 将上载以前由托管代码编写为 .dll 文件的程序集，以便在 SQL Server 实例中使用。  
 
启用时，`CREATE ASSEMBLY` 和 `ALTER ASSEMBLY` 语句中的 `PERMISSION_SET` 选项在运行时将被忽略，但元数据中将保留 `PERMISSION_SET` 选项。 忽略选项可最大程度减少中断现有代码语句。
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许使用相同的名称、区域性和公钥来注册程序集的不同版本。  
  
在尝试访问在指定的程序集时\<client_assembly_specifier >，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]模拟当前的 Windows 登录名的安全上下文。 如果\<client_assembly_specifier > 指定的网络位置 （UNC 路径），当前登录名的模拟将不会传递到网络位置由于委派限制。 在这种情况下，将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户的安全上下文进行访问。 有关详细信息，请参阅[凭据 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)。
  
 除了通过指定的根程序集*程序集 _ 名称*，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]尝试上载任何由正在上载的根程序集引用的程序集。 如果前面的 CREATE ASSEMBLY 语句已将被引用的程序集上载到数据库中，则不再上载此程序集，但它仍可用于根程序集。 如果以前未上载相关程序集，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法在源目录中找到它的清单文件，则 CREATE ASSEMBLY 将返回错误。  
  
 如果根程序集引用的所有相关程序集尚未在数据库中并且与根程序集一起隐式加载，则它们与根级别程序集具有相同的权限设置。 如果必须使用不同于根级别程序集的权限设置创建相关程序集，则它们必须在具有相应权限设置的根级别程序集之前显式上载。  
  
## <a name="assembly-validation"></a>程序集验证  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将对 CREATE ASSEMBLY 语句上载的程序集二进制文件执行检查，以确保符合以下要求：  
  
-   程序集二进制文件具有格式正确的有效元数据和代码段，并且代码段包含有效的 Microsoft 中间语言 (MSIL) 指令。  
  
-   所引用的一组系统程序集是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中以下支持的程序集之一：Microsoft.Visualbasic.dll、Mscorlib.dll、System.Data.dll、System.dll、System.Xml.dll、Microsoft.Visualc.dll、Custommarshallers.dll、System.Security.dll、System.Web.Services.dll、System.Data.SqlXml.dll、System.Core.dll 和 System.Xml.Linq.dll。 还可引用其他系统程序集，但这些程序集必须在数据库中显式注册。  
  
-   对于使用 SAFE 或 EXTERNAL ACCESS 权限集创建的程序集：  
  
    -   程序集代码应是类型安全的。 通过对程序集运行公共语言运行时验证工具可建立类型安全。  
  
    -   程序集的类中不应包含任何静态数据成员，除非这些成员标记为只读。  
  
    -   程序集中的类不能包含终结器方法。  
  
    -   程序集的类或方法只能使用允许的代码属性进行注释。 有关详细信息，请参阅[对于 CLR 例程的自定义特性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
 除了执行 CREATE ASSEMBL 时进行的上述检查外，在执行程序集中代码时还应进行其他检查：  
  
-   调用某些[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]需要特定的代码访问权限的 Api 可能会失败，如果程序集的权限集不包含该权限。  
  
-   对于 SAFE 和 EXTERNAL_ACCESS 程序集，对使用某些 HostProtectionAttribute 注释的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API 的任何调用尝试都将失败。  
  
 有关详细信息，请参阅[设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
## <a name="permissions"></a>权限  
 需要 CREATE ASSEMBLY 权限。  
  
 如果的 PERMISSION_SET = EXTERNAL_ACCESS 指定，则需要**EXTERNAL ACCESS ASSEMBLY**服务器上的权限。 如果的 PERMISSION_SET = UNSAFE 指定，则需要**UNSAFE ASSEMBLY**服务器上的权限。  
  
 如果程序集已经存在于数据库中，则用户必须是将上载的程序集所引用的所有程序集的所有者。 若要使用的文件路径来上载程序集，当前用户必须是 Windows 身份验证登录名或属于**sysadmin**固定的服务器角色。 执行 CREATE ASSEMBLY 的用户的 Windows 登录名必须对此语句中加载的共享和文件具有读取权限。  

### <a name="permissions-with-clr-strict-security"></a>CLR 严格的安全权限    
启用 `CLR strict security` 时，创建 CLR 程序集需要以下权限：

- 用户必须具有 `CREATE ASSEMBLY` 权限  
- 并且，还必须满足以下条件之一：  
  - 使用具有相应登录名（该登录名对应于服务器上的 `UNSAFE ASSEMBLY` 权限）的证书或非对称密钥对程序集进行签名。 建议对程序集进行签名。  
  - 数据库的 `TRUSTWORTHY` 属性设置为 `ON`，且数据库由在服务器上具有 `UNSAFE ASSEMBLY` 权限的登录名所有。 不建议使用此选项。  
  
 有关程序集的权限集的详细信息，请参阅[设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="example-a-creating-an-assembly-from-a-dll"></a>示例 a： 从 dll 中创建程序集  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 以下示例假定：[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]示例安装在本地计算机的默认位置，且 HelloWorld.csproj 示例应用程序已编写。 有关详细信息，请参阅[Hello World 示例](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)。  
  
```  
CREATE ASSEMBLY HelloWorld   
FROM <system_drive>:\Program Files\Microsoft SQL Server\100\Samples\HelloWorld\CS\HelloWorld\bin\debug\HelloWorld.dll  
WITH PERMISSION_SET = SAFE;  
```  
  
### <a name="example-b-creating-an-assembly-from-assembly-bits"></a>示例 b： 从程序集 bits 创建程序集  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将替换为你的程序集 bits 示例位 （这是不完整或有效）。  
  
```  
CREATE ASSEMBLY HelloWorld  
    FROM 0x4D5A900000000000  
WITH PERMISSION_SET = SAFE;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER ASSEMBLY &#40;Transact SQL &#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [删除程序集 &#40;Transact SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [使用方案和示例的公共语言运行时 &#40;CLR &#41;集成](http://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
  
  
