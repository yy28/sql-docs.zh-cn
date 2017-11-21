---
title: "FULLTEXTSERVICEPROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FULLTEXTSERVICEPROPERTY_TSQL
- FULLTEXTSERVICEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- FULLTEXTSERVICEPROPERTY function
- services [SQL Server], full-text search properties
- test
ms.assetid: b7dcacb0-af83-4807-9d1e-49148b56b59c
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b40c8cc7070c3cd459cf6fff99854942544f7459
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="fulltextserviceproperty-transact-sql"></a>FULLTEXTSERVICEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回与全文引擎属性有关的信息。 这些属性可以设置并通过使用检索**sp_fulltext_service**。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
FULLTEXTSERVICEPROPERTY ('property')  
```  
  
## <a name="arguments"></a>参数  
 *属性*  
 包含全文服务级别属性名称的表达式。 下表列出了这些属性，并提供对返回的信息的说明。  
  
> [!NOTE]  
>  未来版本中将删除以下属性[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **ConnectTimeout**， **DataTimeout**，和**ResourceUsage**。 应避免在新的开发工作中使用这些属性，并着手修改当前使用上述任意属性的应用程序。  
  
|属性|值|  
|--------------|-----------|  
|**ResourceUsage**|返回 0。 支持它仅仅是为了保持向后兼容。|  
|**ConnectTimeout**|返回 0。 支持它仅仅是为了保持向后兼容。|  
|**IsFulltextInstalled**|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例中安装全文组件。<br /><br /> 0 = 未安装全文组件。<br /><br /> 1 = 已安装全文组件。<br /><br /> NULL = 输入无效或发生错误。|  
|**DataTimeout**|返回 0。 支持它仅仅是为了保持向后兼容。|  
|**LoadOSResources**|指示此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中是否注册并使用了操作系统断字符和筛选器。 默认情况下，禁用此属性，以防止更新程序因疏忽而对操作系统 (OS) 的行为进行更改。 如果允许使用 OS 资源，则可以访问在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 索引服务中注册的语言和文档类型的资源，但不能安装特定于实例的资源。 如果在启用的操作系统资源加载，确保是否受信任的已签名二进制文件; 操作系统资源否则，它们不能加载时**VerifySignature**设置为 1。<br /><br /> 0 = 仅使用特定于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的筛选器和断字符。<br /><br /> 1 = 加载 OS 筛选器和断字符。|  
|**VerifySignature**|指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 服务是否仅加载已签名的二进制文件。 默认情况下，仅加载已签名的可信二进制文件。<br /><br /> 0 = 不检查二进制文件是否已签名。<br /><br /> 1 = 验证是否仅加载了已签名的可信二进制文件。|  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="examples"></a>示例  
 以下示例检查是否仅加载已签名的二进制文件，并且返回值指示未在进行此验证。  
  
```  
SELECT fulltextserviceproperty('VerifySignature');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
0  
```  
  
 请注意，若要将签名验证重新设置为其默认值 1，您可以使用以下 `sp_fulltext_service` 语句：  
  
```  
EXEC sp_fulltext_service @action='verify_signature', @value=1;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [FULLTEXTCATALOGPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_fulltext_service (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
  

