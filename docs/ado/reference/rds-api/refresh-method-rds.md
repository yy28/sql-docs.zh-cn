---
title: "刷新方法 (RDS) |Microsoft 文档"
ms.technology: drivers
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
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords: Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5730f11f027cf6fb4492f8133f88ce80ac35aee3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="refresh-method-rds"></a>刷新方法 (RDS)
将重新查询中指定的数据源[连接](../../../ado/reference/rds-api/connect-property-rds.md)属性和更新查询结果。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
## <a name="remarks"></a>Remarks  
 必须设置[连接](../../../ado/reference/rds-api/connect-property-rds.md)，[服务器](../../../ado/reference/rds-api/server-property-rds.md)，和[SQL](../../../ado/reference/rds-api/sql-property.md)属性在使用之前**刷新**方法。 使用关联的窗体上的所有数据绑定控件**rds.DataControl**对象将反映新的记录集。 预先存在的任何[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)在释放对象，任何未保存的更改将被丢弃。 **刷新**方法自动使第一条记录的当前记录。  
  
 它是一个好办法调用**刷新**方法定期当你处理的数据。 如果检索数据，然后将其保留在客户端计算机上一段时间，则很可能变得过期。 很可能你所做的任何更改将失败，因为其他人可能已更改的记录和提交更改之前。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [刷新方法示例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [刷新方法示例 (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [正在执行方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [刷新方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


