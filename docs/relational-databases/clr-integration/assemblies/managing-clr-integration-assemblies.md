---
title: "管理 CLR 集成程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e95209ed47c5e49177ae43bc9bf5ae1026ca511
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="managing-clr-integration-assemblies"></a>管理 CLR 集成程序集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]托管的代码在编译，然后部署以称为程序集的单位。 程序集将打包为 DLL 或可执行 (.exe) 文件。 尽管可执行文件可以自动运行，但 DLL 必须在现有应用程序中承载。 可以加载到托管的 DLL 程序集，并将其由承载[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 要求首先使用 CREATE ASSEMBLY 语句在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中注册该程序集，然后才能将其加载到进程中并使用它。 还可以使用 ALTER ASSEMBLY 语句从更新的版本更新程序集，或者使用 DROP ASSEMBLY 语句从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中删除程序集。  
  
 程序集信息存储在**sys.assembly_files**已安装的程序集的数据库中的表。 **Sys.assembly_files**表包含以下列。  
  
|列|Description|  
|------------|-----------------|  
|assembly_id|为程序集定义的标识符。 此编号分配到与同一程序集相关的所有对象。|  
|name|对象的名称。|  
|file_id|一个数字，指明每个对象，与关联的第一个对象与给定**assembly_id**正在给定值为 1。 如果多个对象具有相同关联**assembly_id**，然后每个后续**file_id**值就会递增 1。|  
|content|程序集或文件的十六进制表示形式。|  
  
## <a name="in-this-section"></a>本节内容  
 [创建程序集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 介绍如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中创建 SAFE、EXTERNAL_ACCESS 和 UNSAFE CLR 程序集。  
  
 [改变程序集](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 介绍如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中更新 CLR 程序集。  
  
 [删除程序集](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 介绍如何从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中删除 CLR 程序集。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
