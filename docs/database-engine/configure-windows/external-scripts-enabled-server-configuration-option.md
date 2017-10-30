---
title: "external scripts enabled 服务器配置选项 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 74f73ab33a010583b4747fcc2d9b35d6cdea14a2
ms.openlocfilehash: 282f50334b59e2d41e2fcac7e33835859bdffe12
ms.contentlocale: zh-cn
ms.lasthandoff: 08/04/2017

---
# <a name="external-scripts-enabled-server-configuration-option"></a>启用了外部脚本的服务器配置选项
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  使用 **external scripts enabled** 选项启用包含某些远程语言扩展的脚本执行。 此属性默认处于禁用状态。 安装“高级分析服务”后，安装程序可以根据需要将此属性设置为 true。  
  

 在使用 **sp_execute_external_script** 过程执行外部脚本之前，必须启用“已启用外部脚本”选项。 使用 **sp_execute_external_script** 执行受支持的语言（如 R）编写的脚本。在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 由与 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]一起安装的服务器组件工作站工具集和将数据科学家与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]高性能环境相连的连接库构成。  在 **安装程序安装期间安装** 高级分析扩展 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，以启用 R 脚本的执行。 有关详细信息，请参阅 [Installing Previous Versions of SQL Server R Services](http://msdn.microsoft.com/library/48380645-9e72-4744-bebb-1c1fd8a18c43)。  
  
 若要启用外部脚本，请执行下面的脚本：  
  
```  
sp_configure 'external scripts enabled', 1;  
RECONFIGURE WITH OVERRIDE;  
```  
  
 你必须重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以使此更改生效。  
  
## <a name="see-also"></a>另请参阅  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  

