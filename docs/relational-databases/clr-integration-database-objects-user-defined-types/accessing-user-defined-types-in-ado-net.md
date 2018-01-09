---
title: "访问在 ADO.NET 中的用户定义类型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab92bd954e06ffcb3047c77d49d1e142ff5ab861
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="accessing-user-defined-types-in-adonet"></a>在 ADO.NET 中访问用户定义类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用任何支持的语言编写用户定义类型 (Udt) [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 生成可验证代码。 这包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic。 使用 UDT 可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储对象和自定义数据结构。 数据公开为 .NET Framework 类或结构的公共成员，行为则由类或结构的方法来定义。 UDT 可以用作表的列定义为中的变量[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理，或作为自变量的[!INCLUDE[tsql](../../includes/tsql-md.md)]函数或存储的过程。  
  
 在 ADO.NET 中， **System.Data.SqlClient**提供程序通过以下方式公开 Udt:  
  
-   通过**System.Data.SqlClient.SqlDataReader**作为对象。  
  
-   通过**SqlDataReader**以原始字节形式。  
  
-   作为参数的**System.Data.SqlClient.SqlParameter**对象。  
  
## <a name="in-this-section"></a>本节内容  
 [检索 UDT 数据](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 介绍如何检索 UDT 数据和如何指定参数。  
  
 [使用 Dataadapter 更新 UDT 的列](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 描述如何使用中的 Udt**数据集**以及如何更新使用的 UDT 数据**Dataadapter**。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
