---
title: 重置方法 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10a2b6814e219072408b644910d93a08e2f7f120
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728301"
---
# <a name="reset-method-rds"></a>Reset 方法 (RDS)
客户端上执行排序或筛选**记录集**基于指定的排序和筛选器属性。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *value*  
 可选。 一个**布尔**值，该值是**True** （默认） 如果你想要当前的"筛选"行集进行筛选。 **False**指示，原始行集进行筛选，删除任何以前的筛选器选项。  
  
## <a name="remarks"></a>备注  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)属性提供排序和筛选功能在客户端缓存。 排序功能的一个列中的值对记录进行排序。 筛选功能显示基于查找条件，同时完整记录的子集[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)维护在缓存中。 **重置**方法将执行条件并将替换当前**记录集**使用可更新**记录集**。  
  
 如果对尚未提交，原始数据的更改**重置**方法将失败。 首先，使用[SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法以将任何更改保存在一个读/写**记录集**，然后使用**重置**方法进行排序或筛选记录。  
  
 如果你想要在行集上执行多个筛选器，则可以使用可选*布尔*自变量与**重置**方法。 下面的示例演示如何执行此操作：  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [FilterColumn、 FilterCriterion、 FilterValue，SortColumn 和 SortDirection 属性和重置方法示例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



