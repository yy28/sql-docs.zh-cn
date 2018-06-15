---
title: 使用 IMultipleResults 处理多个结果集 |Microsoft 文档
description: 使用 IMultipleResults 处理多个结果集
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f23403985aba1fe2ba4e344293ca04eb2322b2c6
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305286"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 处理多个结果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  使用者使用**IMultipleResults**接口来处理通过 OLE DB 驱动程序为 SQL Server 命令执行返回的结果。 当 SQL Server 的 OLE DB 驱动程序提交的命令执行，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]执行的语句并返回任何结果。  
  
 客户端必须处理命令执行返回的所有结果。 因为用于 SQL Server 命令执行的 OLE DB 驱动程序可以生成多个行集对象作为结果，请使用**IMultipleResults**接口，以确保应用程序数据检索完成客户端启动往返过程。  
  
 以下[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句生成多个行集、 从某些包含行数据**OrderDetails**表和 COMPUTE BY 子句的一些包含结果：  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果使用者执行包含该文本的命令并请求行集作为返回的结果接口，则只返回第一组行。 使用者可以处理返回的行集中的所有行。 但是，如果 DBPROP_MULTIPLECONNECTIONS 数据源属性设置为 VARIANT_FALSE 和 MARS 连接上未启用，直到，可以对 （SQL Server 的 OLE DB 驱动程序将创建另一个连接） 的会话对象执行任何其他命令命令都会被取消。 如果在连接上未启用 MARS，SQL Server 的 OLE DB 驱动程序将返回 DB_E_OBJECTOPEN 错误，如果 DBPROP_MULTIPLECONNECTIONS 为 VARIANT_FALSE，并返回 E_FAIL，如果没有活动事务。  
  
 SQL Server 的 OLE DB 驱动程序还将返回 DB_E_OBJECTOPEN 时使用流式处理输出参数，应用程序不占用了之前调用的所有返回的输出参数值**IMultipleResults::GetResults**到获取下一个结果集。 如果未启用 MARS 并且连接正忙于运行命令不会生成行集或生成行集不服务器游标，且如果 DBPROP_MULTIPLECONNECTIONS 数据源属性设置为 VARIANT_TRUE，SQL Server 的 OLE DB 驱动程序创建其他连接，以支持并发命令对象，除非事务处于活动状态，在此情况下它返回一条错误。 事务和锁定是在每个连接的基础上通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 来管理的。 如果生成第二个连接，该独立连接上的命令不能共享锁定。 应通过对其他命令所请求的行保持锁定，小心确保一个命令不会阻塞另一个命令。 如果启用 MARS，连接上可以有多个活动命令；如果使用显式事务，所有命令都共享一个公用事务。  
  
 使用者可以取消命令通过使用[ISSAbort::Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md)或释放命令对象和派生的行集上保留的所有引用。  
  
 使用**IMultipleResults**在所有情况下允许使用者，若要获取生成的命令执行的所有行集，并允许使用者以相应地确定何时取消命令执行和免费的会话对象以供其他命令。  
  
> [!NOTE]  
>  当使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标时，命令执行将创建游标。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 返回游标创建是成功还是失败；因此，与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的往返将在命令执行返回时完成。 每个**GetNextRows**调用随后将成为一次往返过程。 这样，可以存在多个活动命令对象，每个对象分别处理作为服务器游标提取结果的行集。 有关详细信息，请参阅[行集和 SQL Server 游标](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>请参阅  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
