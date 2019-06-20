---
title: 查询方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 92247a31eeb5f3e70b54edfaff33ae15340b9df1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712434"
---
# <a name="query-method-rds"></a>Query 方法 (RDS)
使用有效的 SQL 查询字符串返回[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parameters  
 *Recordset*  
 表示的对象变量**记录集**对象。  
  
 *DataFactory*  
 表示的对象变量[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。  
  
 *“连接”*  
 一个**字符串**值，该值包含服务器连接信息。 它类似于[Connect](../../../ado/reference/rds-api/connect-property-rds.md)属性。  
  
 *“数据集属性”*  
 一个**字符串**，它包含 SQL 查询。  
  
## <a name="remarks"></a>备注  
 查询应使用数据库服务器的 SQL 方言。 如果没有具有已执行的查询的错误，则返回结果状态。 **查询**方法不执行任何语法上检查**查询**字符串。  
  
## <a name="applies-to"></a>适用范围  
 [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>请参阅  
 [DataFactory 对象、Query 方法和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


