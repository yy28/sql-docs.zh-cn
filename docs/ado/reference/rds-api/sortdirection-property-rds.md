---
title: "SortDirection 属性 (RDS) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- SortDirection property [RDS]
ms.assetid: 1d9d8715-e4ad-4ff3-bf7f-f1dc0532d8c2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d0395c390da04314dad0bc886f71333baac7b7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sortdirection-property-rds"></a>SortDirection 属性 (RDS)
指示是按升序还是降序排序顺序。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.SortDirection = value  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *值*  
 A**布尔**值，当设置为**True**，指示升序排序方向。 **False**指示降序排序。  
  
## <a name="remarks"></a>注释  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， **SortDirection**， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)属性提供了排序和筛选功能对客户端缓存。 排序功能的使用某一列中的值对记录进行排序。 筛选功能显示基于时完整的查找条件的记录的子集[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)保留在缓存。 [重置](../../../ado/reference/rds-api/reset-method-rds.md)方法将执行条件，并将当前**记录集**与可更新**记录集**。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [FilterColumn、 FilterCriterion、 FilterValue、 SortColumn，和 SortDirection 属性和重置方法示例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [排序属性](../../../ado/reference/ado-api/sort-property.md)   
 [SortColumn 属性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)



