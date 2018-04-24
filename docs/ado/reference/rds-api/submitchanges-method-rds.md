---
title: SubmitChanges 方法 (RDS) |Microsoft 文档
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
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a297a6f41fe3a191742ef6e92f84ecbc2e971eae
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="submitchanges-method-rds"></a>SubmitChanges 方法 (RDS)
提交挂起的更改的本地缓存而可更新[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)中指定的数据源到[连接](../../../ado/reference/rds-api/connect-property-rds.md)属性或[URL](../../../ado/reference/rds-api/url-property-rds.md)属性。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *DataFactory*  
 表示的对象变量[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。  
  
 *连接*  
 A**字符串**值，该值表示与创建的连接**rds.DataControl**对象的[连接](../../../ado/reference/rds-api/connect-property-rds.md)属性。  
  
 *Recordset*  
 表示的对象变量**记录集**对象。  
  
## <a name="remarks"></a>注释  
 [连接](../../../ado/reference/rds-api/connect-property-rds.md)，[服务器](../../../ado/reference/rds-api/server-property-rds.md)，和[SQL](../../../ado/reference/rds-api/sql-property.md)必须设置属性，然后才能使用**SubmitChanges**方法替换**RDS.DataControl**对象。  
  
 如果调用[正在执行](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法后你调用了**SubmitChanges**为同一**记录集**对象，**正在执行**调用失败，因为所做的更改都已提交。  
  
 成功或同时失败的所有更改来进行修改和所做的更改的全部发送已更改的记录。  
  
 你可以使用**SubmitChanges**仅使用默认**提高**对象。 自定义业务对象不能使用此方法。  
  
 如果**URL**已设置属性， **SubmitChanges**将将更改提交到 URL 指定的位置。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>另请参阅  
 [SubmitChanges 方法示例 (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [正在执行方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



