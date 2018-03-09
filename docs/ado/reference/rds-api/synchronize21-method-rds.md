---
title: "Synchronize21 方法 (RDS) |Microsoft 文档"
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c973d97465963ba865bb768569bf70f70366a1b9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="synchronize21-method-rds"></a>Synchronize21 方法 (RDS)
将给定的记录集与指定与 ADO 2.1 一起使用的连接字符串的数据库同步。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 用于连接到 OLE DB 访问接口将该申请发送的字符串。 如果使用一个处理程序，该处理程序可以编辑或替换连接字符串。  
  
 *HandlerString*  
 该字符串标识要用于此执行的处理程序。 该字符串包含两个部分。 第一部分包含要使用的处理程序的名称 (ProgID)。 字符串的第二部分包含自变量传递到处理程序。 如何解释自变量字符串是特定的处理程序。 两个部分的第一个实例在字符串中的逗号分隔。 参数字符串可以包含额外逗号。 这些参数是可选的。  
  
 *lSynchronizeOptions*  
 同步选项的一个位掩码。  
  
 1 =*UpdateTransact*对数据库更新包装在事务中。 如果有任何更新失败，则中止此事务。  
  
 2 =*RefreshWithUpdate*原因行状态时都不返回*刷新*也不*RefreshConflicts*设置。  
  
 4 =*刷新*使用从数据库的当前数据刷新记录集。 挂起的更新将不会应用于数据库。 如果未设置此位，不会刷新记录集，所有挂起的更新推送到数据库。  
  
 8 =*RefreshConflicts*挂起的更改的任何行无法更新。 使用从数据库的当前数据刷新更新失败的行。  
  
 *ppRecordset*  
 指向要同步的记录集的指针指向的指针。  
  
 *pStatusArray*  
 用于返回受影响的行的行状态的安全数组的一个变体同步。 如果任何以下的同步选项设置不设置： *RefreshWithUpdate*，*刷新*和*RefreshConflicts*。  
  
## <a name="remarks"></a>注释  
 *HandlerString*参数可以为 null。 在这种情况下发生的情况取决于如何配置的 RDS 服务器。 "MSDFMAP.handler"的处理程序字符串指示应使用 Microsoft 提供处理程序 (Msdfmap.dll)。 "MASDFMAP.handler,sample.ini"的处理程序字符串指示应使用 Msdfmap.dll 处理程序和自变量"sample.ini"，应传递到处理程序。 Msdfmap.dll 然后会将自变量解释为一个方向，若要使用 sample.ini 检查连接和查询字符串。  
  
> [!NOTE]
>  **Synchronize21**方法是只需版本[同步方法 (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)。 你需要使用**同步**方法进行通信用 ADO 2.1， **Synchronize21**可以改为调用方法。 功能**同步**ADO 2.5 及更高版本中的方法是在 ADO 2.1 中的相同方法提供的功能的一个超集。  
  
## <a name="applies-to"></a>适用范围  
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


