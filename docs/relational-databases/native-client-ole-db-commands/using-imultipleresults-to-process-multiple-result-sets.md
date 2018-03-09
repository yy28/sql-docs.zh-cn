---
title: "使用 IMultipleResults 处理多个结果集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-commands
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a3d352a423a810dfda61d29b4b595e11cddd9e9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 处理多个结果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用者使用**IMultipleResults**接口来处理返回的结果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序命令执行。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序提交的执行，命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行的语句并返回任何结果。  
  
 客户端必须处理命令执行返回的所有结果。 因为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序命令执行可以生成多个行集对象作为结果，请使用**IMultipleResults**接口，以确保应用程序数据检索完成客户端启动往返。  
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句生成多个行集、 从某些包含行数据**OrderDetails**表和 COMPUTE BY 子句的一些包含结果：  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果使用者执行包含该文本的命令并请求行集作为返回的结果接口，则只返回第一组行。 使用者可以处理返回的行集中的所有行。 但是，如果 DBPROP_MULTIPLECONNECTIONS 数据源属性设置为 VARIANT_FALSE 和 MARS 连接上未启用，可以对会话对象执行任何其他命令 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不会创建另一个连接） 直到命令被取消。 如果连接时，不启用 MARS [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 DB_E_OBJECTOPEN 错误，如果 DBPROP_MULTIPLECONNECTIONS 为 VARIANT_FALSE，并返回 E_FAIL，如果没有活动事务。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序还将返回 DB_E_OBJECTOPEN 时使用流式处理输出参数，应用程序不占用了之前调用的所有返回的输出参数值**IMultipleResults::GetResults**若要获取下一个结果集。 如果未启用 MARS 并且连接正忙于运行的命令不生成行集或者生成的行集不是服务器游标，同时 DBPROP_MULTIPLECONNECTIONS 数据源属性设置为 VARIANT_TRUE，那么 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将创建其他连接来支持并发命令对象，除非某个事务处于活动状态（在此情况下，将返回错误）。 事务和锁定是在每个连接的基础上通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来管理的。 如果生成第二个连接，该独立连接上的命令不能共享锁定。 应通过对其他命令所请求的行保持锁定，小心确保一个命令不会阻塞另一个命令。 如果启用 MARS，连接上可以有多个活动命令；如果使用显式事务，所有命令都共享一个公用事务。  
  
 使用者可以取消命令通过使用[ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)或释放命令对象和派生的行集上保留的所有引用。  
  
 使用**IMultipleResults**在所有情况下允许使用者，若要获取生成的命令执行的所有行集，并允许使用者以相应地确定何时取消命令执行和免费的会话对象以供其他命令。  
  
> [!NOTE]  
>  当使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标时，命令执行将创建游标。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回游标创建是成功还是失败；因此，与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的往返将在命令执行返回时完成。 每个**GetNextRows**调用随后将成为一次往返过程。 这样，可以存在多个活动命令对象，每个对象分别处理作为服务器游标提取结果的行集。 有关详细信息，请参阅[行集和 SQL Server 游标](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
