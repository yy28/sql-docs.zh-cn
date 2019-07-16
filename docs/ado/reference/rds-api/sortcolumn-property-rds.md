---
title: SortColumn 属性 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5a9c3f9f50968f3b5e8085052917397bcd90226
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963395"
---
# <a name="sortcolumn-property-rds"></a>SortColumn 属性 (RDS)
表示要对记录进行排序的列。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *String*  
 一个**字符串**值，该值表示名称或别名作为记录排序依据的列。  
  
## <a name="remarks"></a>备注  
 **SortColumn**， [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)属性提供排序和筛选功能在客户端缓存。 排序功能的一个列中的值对记录进行排序。 筛选功能显示基于查找条件，同时完整记录的子集[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)维护在缓存中。 [重置](../../../ado/reference/rds-api/reset-method-rds.md)方法将执行条件并将替换当前**记录集**使用可更新**记录集**。  
  
 若要作为排序依据**记录集**，必须先保存所有挂起的更改。 如果使用的**rds。DataControl**，可以使用[SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法。 例如，如果你**rds。DataControl**是名为 ADC1，是您的代码`ADC1.SubmitChanges`。 如果使用 ADO**记录集**，可以使用其[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 使用**UpdateBatch**是为建议的方法**记录集**创建与对象[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法。 例如，你的代码可能`myRS.UpdateBatch`或`ADC1.Recordset.UpdateBatch`。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [FilterColumn、 FilterCriterion、 FilterValue，SortColumn 和 SortDirection 属性和重置方法示例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [排序属性](../../../ado/reference/ado-api/sort-property.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





