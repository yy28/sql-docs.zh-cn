---
title: SQL 属性 |Microsoft 文档
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d28a6f127b222c03faa9c287522945999da809e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-property"></a>SQL 属性
指示用于检索查询字符串[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 你可以设置**SQL**在设计时属性[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的对象标记，或在运行时在脚本代码。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parameters  
 *QueryString*  
 A**字符串**包含有效的 SQL 数据请求的值。  
  
 *DataControl*  
 表示的对象变量**rds.DataControl**对象。  
  
## <a name="remarks"></a>注释  
 一般情况下，这是一个 SQL 语句 （使用数据库服务器的方言），如`"Select * from NewTitles"`。 若要确保记录匹配，并可准确地更新，可更新查询必须包含长二进制字段或计算的字段以外的字段。  
  
 **SQL**属性是可选的如果自定义服务器端业务对象检索数据的客户端。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL 的属性示例 (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [连接属性 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [查询方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [刷新方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


