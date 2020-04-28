---
title: 编写扩展存储过程的编程 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 541f24693598d20925dd37d4970c6d9916945793
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032010"
---
# <a name="database-engine-extended-stored-procedures---programming"></a>数据库引擎扩展存储过程 - 编程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 过去，程序员使用开放式数据服务编写服务器应用程序，比如到非 SQL 服务器数据库环境的网关。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持开放式数据服务 API 已过时的部分。 在原始的开放式数据服务 API 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仍然支持的唯一部分是扩展存储过程函数，因此该 API 已重命名为扩展存储过程 API。  
  
 随着诸如分布式查询和 CLR 集成这样更新和功能更强大的技术的出现，对扩展存储过程 API 应用程序的需求已大幅减少。  
  
> [!NOTE]  
>  如果您有现成的网关应用程序，则无法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 附带的 opends60.dll 运行应用程序。 网关应用程序不再受支持。  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>扩展存储过程与 CLR 集成的对比  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，当数据库应用程序开发人员要编写那些很难表达或不可能用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编写的服务器端逻辑时，扩展存储过程 (XP) 为其提供了唯一的机制。 CLR 集成为编写这样的存储过程提供了更可靠的替代选择。 此外，通过使用 CLR 集成，过去经常以存储过程的形式编写的逻辑现在通常可以更好地表达为表值函数，这样就可以将 SELECT 语句嵌入 FROM 子句中从而使用该 SELECT 语句对该函数所构造的结果进行查询。  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时 &#40;CLR&#41; 集成概述](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)   
 [CLR 表值函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
