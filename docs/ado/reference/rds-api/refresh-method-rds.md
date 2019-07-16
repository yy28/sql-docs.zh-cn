---
title: Refresh 方法 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb7cb94edab6b5422c315b71c2900662f85aa1e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963500"
---
# <a name="refresh-method-rds"></a>Refresh 方法 (RDS)
将重新查询中指定的数据源[Connect](../../../ado/reference/rds-api/connect-property-rds.md)属性和更新查询结果。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
## <a name="remarks"></a>备注  
 必须设置[Connect](../../../ado/reference/rds-api/connect-property-rds.md)，[服务器](../../../ado/reference/rds-api/server-property-rds.md)，并[SQL](../../../ado/reference/rds-api/sql-property.md)属性，然后使用**刷新**方法。 使用关联的窗体上的所有数据绑定控件**rds。DataControl**对象将反映新的记录集。 已存在的任何[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)释放对象，并丢弃所有未保存的更改。 **刷新**方法自动使第一条记录的当前记录。  
  
 它是调用一个好办法**刷新**方法定期处理数据。 如果检索数据，然后将其保留在客户端计算机一段时间，则可能会过期。 很可能所做的任何更改将失败，因为其他人可能已更改该记录并提交前您的更改。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [Refresh 方法示例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 方法示例 (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


