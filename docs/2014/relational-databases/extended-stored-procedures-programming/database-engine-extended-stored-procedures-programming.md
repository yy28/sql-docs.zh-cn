---
title: 编写扩展存储的过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bc740b25f875b451168a8c051e6f32bd984fbfe6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62514452"
---
# <a name="programming-extended-stored-procedures"></a>编写扩展存储过程
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 过去，程序员使用开放式数据服务编写服务器应用程序，比如到非 SQL 服务器数据库环境的网关。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持开放式数据服务 API 的过时部分。 在原始的开放式数据服务 API 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仍然支持的唯一部分是扩展存储过程函数，因此该 API 已重命名为扩展存储过程 API。  
  
 随着诸如分布式查询和 CLR 集成这样更新和功能更强大的技术的出现，对扩展存储过程 API 应用程序的需求已大幅减少。  
  
> [!NOTE]  
>  如果您有现成的网关应用程序，则无法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 附带的 opends60.dll 运行应用程序。 网关应用程序不再受支持。  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>扩展存储过程与。CLR 集成的对比  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，当数据库应用程序开发人员要编写那些很难表达或不可能用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编写的服务器端逻辑时，扩展存储过程 (XP) 为其提供了唯一的机制。 CLR 集成为编写这样的存储过程提供了更可靠的替代选择。 此外，通过使用 CLR 集成，过去经常以存储过程的形式编写的逻辑现在通常可以更好地表达为表值函数，这样就可以将 SELECT 语句嵌入 FROM 子句中从而使用该 SELECT 语句对该函数所构造的结果进行查询。  
  
## <a name="see-also"></a>请参阅  
 [公共语言运行时&#40;CLR&#41;集成概述](../clr-integration/common-language-runtime-integration-overview.md)   
 [CLR 表值函数](../clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
