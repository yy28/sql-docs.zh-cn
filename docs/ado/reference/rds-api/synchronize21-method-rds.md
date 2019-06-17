---
title: Synchronize21 方法 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1d731738938eab5732dcbfa86c0d624ae7941ed5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697254"
---
# <a name="synchronize21-method-rds"></a>Synchronize21 方法 (RDS)
将给定的记录集与 ADO 2.1 一起使用的连接字符串由指定的数据库同步。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 用于连接到 OLE DB 访问接口将请求发送的字符串。 如果使用一个处理程序，该处理程序可以编辑或替换连接字符串。  
  
 *HandlerString*  
 该字符串标识要用于此执行的处理程序。 该字符串包含两个部分。 第一部分包含要使用的处理程序的名称 (ProgID)。 字符串的第二部分包含自变量传递给处理程序。 如何解释自变量字符串是特定的处理程序。 两个部分分隔字符串中逗号的第一个实例。 参数字符串可以包含额外逗号。 这些参数是可选的。  
  
 *lSynchronizeOptions*  
 同步选项的位掩码。  
  
 1 =*UpdateTransact*对数据库的更新都包装在事务中。 如果有任何更新失败，该事务被中止。  
  
 2 =*RefreshWithUpdate*原因行状态时都不返回*刷新*也不*RefreshConflicts*设置。  
  
 4 =*刷新*当前数据库中的数据刷新记录集。 挂起的更新不推送到数据库。 如果未设置此位，则不刷新记录集和所有挂起的更新推送到数据库。  
  
 8 =*RefreshConflicts*挂起的更改的任何行未能更新。 当前数据库中的数据刷新失败更新的行。  
  
 *ppRecordset*  
 指向要同步的记录集的指针指向的指针。  
  
 *pStatusArray*  
 用于返回受影响的行的行状态的安全数组的变体同步。 未设置，如果没有以下同步选项的设置：*RefreshWithUpdate*，*刷新*并*RefreshConflicts*。  
  
## <a name="remarks"></a>备注  
 *HandlerString*参数可以为 null。 在这种情况下发生的情况取决于如何配置 RDS 服务器。 "MSDFMAP.handler"的处理程序字符串指示应使用 Microsoft 提供处理程序 (Msdfmap.dll)。 "MASDFMAP.handler,sample.ini"的处理程序字符串指示应使用 Msdfmap.dll 处理程序和自变量"sample.ini"，应传递给处理程序。 Msdfmap.dll 然后会将自变量解释为方向使用 sample.ini 检查连接和查询字符串。  
  
> [!NOTE]
>  **Synchronize21**方法是只需版本[同步方法 (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)。 需要使用**Synchronize**方法以与 ADO 2.1，通信**Synchronize21**改为调用方法。 功能**同步**ADO 2.5 及更高版本中的方法是在 ADO 2.1 中的相同方法所提供的功能的一个超集。  
  
## <a name="applies-to"></a>适用范围  
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


