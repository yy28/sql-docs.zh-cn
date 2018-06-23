---
title: 目录属性对话框中 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.ssms.iscatalogprop.general.f1
- sql12.ssis.ssms.iscreatecatalog.f1
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7eb8991b7545b19b04b3626e741ad2fdebd12c48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125421"
---
# <a name="catalog-properties-dialog-box"></a>“目录属性”对话框
  使用“目录属性”对话框可以配置 SSISDB 目录。 目录属性定义如何对敏感数据进行加密、如何保留操作和项目版本控制数据以及验证操作何时超时。SSISDB 目录是用于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目、包、参数和环境的中心存储区和管理点。  
  
 您还可以在 catalog.catalog_property 视图中查看目录属性，并且通过使用 catalog.configure_catalog 存储过程设置属性。 有关详细信息，请参阅 [catalog.catalog_properties（SSISDB 数据库）](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database)和 [catalog.configure_catalog（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)。  
  
 有关如何创建 SSISDB 目录的信息，请参阅[创建 SSIS 目录](catalog/ssis-catalog.md)。  
  
 **您希望做什么？**  
  
-   [打开“目录属性”对话框](#open_dialog)  
  
-   [配置选项](#options)  
  
##  <a name="open_dialog"></a> 打开“目录属性”对话框  
  
1.  打开[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
2.  连接到 Microsoft SQL Server 数据库引擎。  
  
3.  在对象资源管理器中，展开“Integration Services”节点，右键单击“SSISDB”，然后单击“属性”。  
  
##  <a name="options"></a> 配置选项  
  
### <a name="options"></a>“常规”  
 下表描述该对话框中的某些属性以及 catalog.catalog_property 视图中的相应属性。  
  
|属性名称（“目录属性”对话框）|属性名称（catalog.catalog_property 视图）|Description|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|加密算法名称|ENCRYPTION_CLEANUP_ENABLED|指定用于对于目录中的敏感参数值进行加密的加密类型。 下面是可能的值：<br /><br /> **DES**<br /><br /> **TRIPLE_DES**<br /><br /> **TRIPLE_DES_3KEY**<br /><br /> **DESPX**<br /><br /> **AES_128**<br /><br /> **AES_192**<br /><br /> **AES_256** （默认值）|  
|验证超时（秒）|VALIDATION_TIMEOUT|指定项目验证或包验证可运行的最大秒数，超过该秒数后运行将停止。 默认值为 300 秒。<br /><br /> 执行验证是一个异步操作。 项目或包越大，验证所用的时间就会越长。<br /><br /> 有关验证项目和包的信息，请参阅 [Integration Services Data Types in Expressions](expressions/integration-services-data-types-in-expressions.md)。|  
|定期清理日志|OPERATION_CLEANUP_ENABLED|将该属性设置为 True 可指示 SQL Server 代理作业“操作清除”运行。 否则，将该属性设置为 False。|  
|保持期(天)|RETENTION_WINDOW|指定可允许操作数据的最长时间（天）。 早于该指定天数的数据将由 SQL 代理作业“操作清除”删除。|  
|每个项目的最大版本数|MAX_PROJECT_VERSIONS|指定在目录中将存储项目的多少个版本。 在项目版本清除作业运行时，超过该最大值的项目的更早的版本将被删除。|  
  
  
