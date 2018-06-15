---
title: ADOMD.NET Server 功能 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 003e50efa8ed21720410830a3d02134df15c3c97
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023774"
---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET 服务器功能
  所有 ADOMD.NET 服务器对象都可对服务器上的数据和元数据提供只读访问。 若要检索数据和元数据，则可使用 ADOMD.NET 服务器对象模型，因为该服务器对象模型不支持架构行集。  
  
 使用 ADOMD.NET server 对象，您可以创建用户定义函数 (UDF) 或存储的过程作为[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 这些进程内方法是通过使用多维表达式 (MDX)、数据挖掘扩展插件 (DMX) 或 SQL 之类的语言创建的查询语句调用的。 这些进程内方法还可提供附加功能而不会有网络通信的延迟。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 对象仅支持 DMX。  
  
## <a name="what-is-a-udf"></a>什么是 UDF？  
 A *UDF*是一种方法具有以下特征：  
  
-   可以在查询上下文中调用 UDF。  
  
-   UDF 可以使用任意数量的参数。  
  
-   UDF 可以返回各种类型的数据。  
  
 下面的示例使用了虚拟的 UDF `FinalSalesNumber`：  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>什么是存储过程？  
 A*存储过程*是一种方法具有以下特征：  
  
-   在调用存储的过程上使用 MDX 自己[调用](../../mdx/mdx-data-manipulation-call.md)语句。  
  
-   存储过程可以使用任意数量的参数。  
  
-   存储的过程可以返回数据集， **IDataReader**，结果为空。  
  
 下面的示例使用了虚拟的存储过程 `FinalSalesNumbers`：  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 服务器编程](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
