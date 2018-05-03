---
title: 记录集，SourceRecordset 属性 (RDS) |Microsoft 文档
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
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e934983f54be5644e945e4ecdcf201b793c33ea4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-sourcerecordset-properties-rds"></a>记录集，SourceRecordset 属性 (RDS)
指示**记录集**从自定义业务对象返回的对象。  
  
 **适用于：** [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *Recordset*  
 表示的对象变量**记录集**对象。  
  
## <a name="remarks"></a>注释  
 你可以设置**SourceRecordset**属性[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从自定义业务对象返回。  
  
 这些属性允许应用程序通过自定义过程中处理绑定过程。 它们接收包装在一个行集**记录集**，以便你可以直接与交互**记录集**、 执行操作，例如设置属性或循环访问**记录集**.  
  
 你可以设置**SourceRecordset**属性或阅读**记录集**属性在运行时在脚本代码。  
  
 **SourceRecordset**是只写属性，与此相反**记录集**属性，它是只读属性。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [记录集和 SourceRecordset 属性示例 (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Query 方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


