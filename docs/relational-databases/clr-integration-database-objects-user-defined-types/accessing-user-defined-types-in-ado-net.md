---
title: ADO.NET 中访问用户定义类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 82ccd420318026bddac2979735c514b8b43e4a88
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631085"
---
# <a name="accessing-user-defined-types-in-adonet"></a>在 ADO.NET 中访问用户定义类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  用户定义类型 (Udt) 使用任何支持的语言编写的[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework 公共语言运行时 (CLR) 生成可验证代码。 这包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic。 使用 UDT 可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储对象和自定义数据结构。 数据公开为 .NET Framework 类或结构的公共成员，行为则由类或结构的方法来定义。 UDT 可用作表的列定义、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的变量，还可用作 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数或存储过程的参数。  
  
 在 ADO.NET 中， **System.Data.SqlClient**提供程序中通过以下方式公开 Udt:  
  
-   通过**System.Data.SqlClient.SqlDataReader**作为对象。  
  
-   通过**SqlDataReader**作为原始字节。  
  
-   作为参数的**System.Data.SqlClient.SqlParameter**对象。  
  
## <a name="in-this-section"></a>本节内容  
 [检索 UDT 数据](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 介绍如何检索 UDT 数据和如何指定参数。  
  
 [使用 DataAdapter 更新 UDT 列](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 介绍如何使用中的 Udt**数据集**以及如何更新 UDT 数据使用**Dataadapter**。  
  
## <a name="see-also"></a>请参阅  
 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
