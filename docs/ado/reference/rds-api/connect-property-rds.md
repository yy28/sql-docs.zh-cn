---
title: 连接属性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: abf2b751f6f1e89cf51560ad7e0d38aa05da7b8b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851462"
---
# <a name="connect-property-rds"></a>Connect 属性 (RDS)
指示在其上运行的查询和更新操作的数据库名称。  
  
 可以设置**Connect**在设计时属性[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的对象标记，或在运行时在脚本代码 (例如，VBScript) 中。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 有效的连接字符串。 有关连接字符串的更多常规信息，请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性或提供程序文档。  
  
> [!NOTE]
>  为提供程序指定 MS 远程**rds。DataControl**将创建四个层方案。 方案大于三个层尚未经过测试，并应不必需的。  
  
 *DataControl*  
 表示的对象变量**rds。DataControl**对象。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [Connect 属性示例 (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [查询方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


