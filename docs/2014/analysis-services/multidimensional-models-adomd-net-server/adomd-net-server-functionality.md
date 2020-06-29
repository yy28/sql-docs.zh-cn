---
title: ADOMD.NET 服务器功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
author: minewiskan
ms.author: owend
ms.openlocfilehash: f00215c6bcc0104c920be29e0837288a469b252e
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469072"
---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET 服务器功能
  所有 ADOMD.NET 服务器对象都可对服务器上的数据和元数据提供只读访问。 若要检索数据和元数据，则可使用 ADOMD.NET 服务器对象模型，因为该服务器对象模型不支持架构行集。  
  
 使用 ADOMD.NET 服务器对象，可以创建用户定义的函数（UDF）或存储过程 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 这些进程内方法是通过使用多维表达式 (MDX)、数据挖掘扩展插件 (DMX) 或 SQL 之类的语言创建的查询语句调用的。 这些进程内方法还可提供附加功能而不会有网络通信的延迟。  
  
> [!NOTE]  
>  [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. AdomdCommand](/previous-versions/sql/sql-server-2014/ms143286(v=sql.120))对象仅支持 DMX。  
  
## <a name="what-is-a-udf"></a>什么是 UDF？  
 *UDF*是一种具有以下特征的方法：  
  
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
 *存储过程*是一种具有以下特征的方法：  
  
-   您可以使用 MDX [call](/sql/mdx/mdx-data-manipulation-call)语句自行调用存储过程。  
  
-   存储过程可以使用任意数量的参数。  
  
-   存储过程可以返回数据集、`IDataReader` 或空结果。  
  
 下面的示例使用了虚拟的存储过程 `FinalSalesNumbers`：  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 服务器编程](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
