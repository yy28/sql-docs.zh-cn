---
title: FilterCriterion 属性（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 88e1bbdb45b48e42d69bd921384056089b3a2241
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82752029"
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion 属性 (RDS)
指示要在筛选器值中使用的求值运算符。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>参数  
 *DataControl*  
 表示 RDS 的对象变量[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *字符串*  
 一个**字符串**值，该值指定[FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)对记录的求值运算符。 可以是以下任一项： <、 \< =、>、>=、= 或 <>。  
  
## <a name="remarks"></a>备注  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 **FilterCriterion**和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)属性提供客户端缓存上的排序和筛选功能。 排序功能按一个列中的值对记录进行排序。 筛选功能显示基于查找条件的记录子集，而完整的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)则保留在缓存中。 [Reset](../../../ado/reference/rds-api/reset-method-rds.md)方法将执行条件，并将当前**记录集**替换为可更新的**记录集**。  
  
 "！ =" 运算符对于**FilterCriterion**无效;请改用 "<>"。  
  
 如果同时设置了筛选和排序属性，并调用**Reset**方法，则首先筛选行集，然后对行集进行排序。 对于升序排序，空值位于顶部;对于降序排序，空值位于底部（升序为默认行为）。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 属性和 Reset 方法示例（VBScript）](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 属性（RDS）](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue 属性（RDS）](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 属性（RDS）](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


