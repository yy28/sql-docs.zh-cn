---
title: 执行方法 (RDS) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 488b4056ca768cfae943558aefc9922bd1a16368
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288182"
---
# <a name="execute-method-rds"></a>执行方法 (RDS)
执行该请求，并使用 ADO 记录集在创建 ADO 2.5 及更高版本。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 用于连接到 OLE DB 提供程序请求执行的发送位置的字符串。 如果处理程序指定使用*HandlerString*它可以编辑或替换连接字符串。  
  
 *HandlerString*  
 用于标识要用于此执行的处理程序的两部分字符串。 该字符串包含两个部分。 第一部分包含要使用的处理程序的名称 (ProgID)。 第二部分包含自变量传递到处理程序。 如何解释自变量字符串的详细信息是特定于每个处理程序。 两个部分的第一个实例在字符串中的逗号分隔。 参数字符串可以包含额外逗号。 这些参数是可选的。  
  
 *QueryString*  
 在连接字符串中标识的 OLE DB 访问接口支持的命令语言中的命令。 对于基于 SQL 的提供程序， *QueryString*可能包含 TRANSACT-SQL 命令语句，但对于非 SQL 提供程序 (例如，MSDataShape)，这可能不是[!INCLUDE[tsql](../../../includes/tsql_md.md)]查询语句。  
  
 如果正在使用一个处理程序，该处理程序可以更改或替换此处指定的值。 例如，该处理程序通常取代*QueryString*其.ini 文件中的查询字符串。 默认情况下，使用 Msdfmap.ini 文件。  
  
 *lFetchOptions*  
 指示异步获取数据的类型。  
  
 有关详细信息，请参阅[FetchOptions 属性 (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)。  
  
 *TableID*  
 A **Variant**类型的 VT_EMPTY 或 VT_BSTR。 如果此值的类型是 VT_EMPTY，则忽略它。 如果类型 VT_BSTR 的是，通过创建记录集**adCmdTableDirect**和此处指定的值与*QueryString*参数将被忽略。  
  
 *lExecuteOptions*  
 执行选项一个位掩码：  
  
 1 =*ReadOnly*将使用打开记录集**adLockReadOnly**。  
  
 2 =*NoBatch*将使用打开记录集**adLockOptimistic**。  
  
 4 =*AllParamInfoSupplied*调用方保证中提供的所有参数的参数信息*pParameters*。  
  
 8 =*GetInfo*将从 OLE DB 提供程序获取查询的参数信息，并将其在中返回*pParameters*参数。 不执行查询并返回任何记录集。  
  
 16 =*GetHiddenColumns*将使用打开记录集**adLockBatchOptimistic**和任何隐藏的列将包含在记录集。  
  
 *ReadOnly*， *NoBatch*和*GetHiddenColumns*是相互排斥的选项; 但是，它不生成错误设置多个。 如果设置了多个选项， *GetHiddenColumns*优先于所有其他成员后, 跟*ReadOnly*。 如果未不指定任何选项，默认情况下，通过打开记录集**adLockBatchOptimistic**和隐藏的列不包含在记录集。  
  
 *pParameters*  
 A **Variant**包含安全数组的参数定义。 如果*GetInfo*选项中指定*lExecuteOptions*，此参数用于返回从 OLE DB 提供程序获取的参数定义。 否则，此参数可以为空。  
  
 *lcid*  
 LCID 用于生成中返回任何错误*pInformation*。  
  
 *pInformation*  
 指向返回执行的信息错误的指针。 如果为 NULL，则不返回任何错误的信息。  
  
## <a name="remarks"></a>Remarks  
 *HandlerString*参数可以为 null。 在这种情况下发生的情况取决于如何配置的 RDS 服务器。 "MSDFMAP.handler"的处理程序字符串指示应使用 Microsoft 提供处理程序 (Msdfmap.dll)。 "MASDFMAP.handler,sample.ini"的处理程序字符串指示应使用 Msdfmap.dll 处理程序和自变量"sample.ini"，应传递到处理程序。 MSDFMAP.dll 将解释为一个方向，若要使用 sample.ini 检查连接和查询字符串参数。  
  
## <a name="applies-to"></a>适用范围  
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


