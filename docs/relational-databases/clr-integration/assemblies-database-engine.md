---
title: 程序集（数据库引擎） |Microsoft Docs
description: SQL Server 实例可以承载部署函数、过程、触发器、用户定义聚合和使用 CLR 语言编写的类型的程序集。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
ms.openlocfilehash: 386e1980ae19ba4f98222b51a4955b024f815083
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488066"
---
# <a name="assemblies-database-engine"></a>程序集（数据库引擎）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本节中的主题旨在帮助您了解、设计和实现程序集。  
  
 程序集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是用于部署函数、存储过程、触发器、用户定义聚合和用户定义类型（以[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时（CLR）托管的一种托管代码语言，而不是在中[!INCLUDE[tsql](../../includes/tsql-md.md)]）的 DLL 文件。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的程序集对象引用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 公共语言运行时中创建的托管应用程序模块（.dll 文件）。 程序集包含类元数据和托管代码。 将程序集上载到 SQL Server 实例是创建以下任何一个数据库对象的第一步：  
  
-   CLR 函数。 有关详细信息，请参阅[创建 CLR 函数](../../relational-databases/user-defined-functions/create-clr-functions.md)。  
  
-   CLR 存储过程。 有关详细信息，请参阅[CLR 存储过程](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)。  
  
-   CLR 触发器。 有关详细信息，请参阅[创建 CLR 触发器](../../relational-databases/triggers/create-clr-triggers.md)。  
  
-   用户定义聚合函数。 有关详细信息，请参阅[创建用户定义聚合](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)。  
  
-   用户定义类型。 有关详细信息，请参阅[使用用户定义类型](../../relational-databases/native-client/features/using-user-defined-types.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中程序集可以执行下列功能：  
  
-   包含可以实现已列出的一个或多个 CLR 数据库对象的功能的托管代码。  
  
-   包含程序集以下方面的元数据：版本号和区域性、唯一标识类列表的可选公钥、定义的方法以及处理器体系结构。  
  
-   通过控制代码访问权限，管理托管代码可以访问外部资源的等级。  
  
-   包含有关程序集与所引用的其他程序集之间的依赖关系的元数据。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)|说明创建程序集之前必须考虑的问题， 包括打包程序集、代码访问权限和其他限制。|  
|[实现程序集](../../relational-databases/clr-integration/assemblies-implementing.md)|说明如何创建和删除程序集、如何以及何时修改程序集、如何检索程序集的有关元数据。|  
|[获取有关程序集的信息](../../relational-databases/clr-integration/assemblies-getting-information.md)|列出了可以查询程序集的有关元数据的目录视图和函数。|  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时 (CLR) 集成编程概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
