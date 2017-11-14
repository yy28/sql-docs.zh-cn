---
title: "连接属性 (RDS) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46668b0b90099994724e39dc5f9d911431e6fd85
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connect-property-rds"></a>连接属性 (RDS)
指示从中运行的查询和更新操作的数据库名称。  
  
 你可以设置**连接**在设计时属性[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的对象标记，或在运行时在脚本代码 (例如，VBScript)。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 有效的连接字符串。 有关连接字符串的更多常规信息，请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性或提供程序文档。  
  
> [!NOTE]
>  指定为的提供程序的 MS 远程**rds.DataControl**将创建四个层方案。 方案大于三个层没有进行测试和应不必需的。  
  
 *DataControl*  
 表示的对象变量**rds.DataControl**对象。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [连接属性示例 (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [查询方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [刷新方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



