---
title: FilterColumn 属性（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterColumn property [ADO]
ms.assetid: 0a5473e8-8ce6-4518-83fb-4920b827e285
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e88cb6f8d563df66a8faaa84d5aeafaa9d359e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964085"
---
# <a name="filtercolumn-property-rds"></a>FilterColumn 属性 (RDS)
指示用于计算筛选条件的列。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.FilterColumn = String  
```  
  
#### <a name="parameters"></a>参数  
 *DataControl*  
 表示 RDS 的对象变量[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *字符串*  
 一个**字符串**值，该值指定要对其计算筛选条件的列。 筛选条件是在[FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)属性中指定的。  
  
## <a name="remarks"></a>备注  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)和**FilterColumn**属性提供客户端缓存上的排序和筛选功能。 排序功能按一个列中的值对记录进行排序。 筛选功能显示基于查找条件的记录子集，而完整的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)则保留在缓存中。 [Reset](../../../ado/reference/rds-api/reset-method-rds.md)方法将执行条件，并将当前**记录集**替换为可更新的**记录集**。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 属性和 Reset 方法示例（VBScript）](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterCriterion 属性（RDS）](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [FilterValue 属性（RDS）](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 属性（RDS）](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


