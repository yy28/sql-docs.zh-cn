---
title: I多倍结果，多个结果集
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5e19cef4e00fc1c55e29e51ccea13c2fdb7a0e2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304438"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 处理多个结果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  使用者使用**IMulti结果**接口来处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序命令执行返回的结果。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序提交执行命令时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行语句并返回任何结果。  
  
 客户端必须处理命令执行返回的所有结果。 由于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序提供程序命令执行可以生成多个行集对象作为结果，因此使用**IMulti结果**接口确保应用程序数据检索完成客户端启动的往返。  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句生成多个行集，某些行集包含 OrderDetails 表的行数据，某些行集包含 COMPUTE BY 子句的结果****：  
  
```sql
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果使用者执行包含该文本的命令并请求行集作为返回的结果接口，则只返回第一组行。 使用者可以处理返回的行集中的所有行。 但是，如果DBPROP_MULTIPLECONNECTIONS数据源属性设置为VARIANT_FALSE，并且未在连接上启用 MARS，则在取消命令之前，无法在会话对象上执行其他命令（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序不会创建其他连接）。 如果在连接上未启用 MARS，则如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_MULTIPLECONNECTIONSVARIANT_FALSE，则本机客户端 OLE DB 提供程序将返回DB_E_OBJECTOPEN错误，如果存在活动事务，则返回E_FAIL。  
  
 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]流式输出参数时，本机客户端 OLE DB 提供程序也将返回DB_E_OBJECTOPEN，并且应用程序在调用**IMultiResult：：getResult**获取下一个结果集之前，未使用所有返回的输出参数值。 如果未启用 MARS 并且连接正忙于运行的命令不生成行集或者生成的行集不是服务器游标，同时 DBPROP_MULTIPLECONNECTIONS 数据源属性设置为 VARIANT_TRUE，那么 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将创建其他连接来支持并发命令对象，除非某个事务处于活动状态（在此情况下，将返回错误）。 事务和锁定是在每个连接的基础上通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来管理的。 如果生成第二个连接，该独立连接上的命令不能共享锁定。 应通过对其他命令所请求的行保持锁定，小心确保一个命令不会阻塞另一个命令。 如果启用 MARS，连接上可以有多个活动命令；如果使用显式事务，所有命令都共享一个公用事务。  
  
 使用者可以使用 [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) 或释放命令对象和派生行集所持有的所有引用来取消命令。  
  
 通过在所有实例中使用 IMultipleResults，使用者能够获取命令执行生成的所有行集，并正确确定何时取消命令执行和释放会话对象以供其他命令使用****。  
  
> [!NOTE]  
>  当使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标时，命令执行将创建游标。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回游标创建是成功还是失败；因此，与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的往返将在命令执行返回时完成。 随后，每个 GetNextRows 调用成为一个往返****。 这样，可以存在多个活动命令对象，每个对象分别处理作为服务器游标提取结果的行集。 有关详细信息，请参阅[行集和 SQL Server 游标](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
