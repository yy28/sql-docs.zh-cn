---
title: FilterValue 属性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a30e3058c86c3250942238b3cd98a0cfd6e0a6de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273744"
---
# <a name="filtervalue-property-rds"></a>FilterValue 属性 (RDS)
指示要用于筛选记录的值。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *String*  
 一个**字符串**值，该值表示用来筛选记录的数据值 (例如，`'Programmer'`或`125`)。  
  
## <a name="remarks"></a>备注  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)， **FilterValue**， [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)属性提供排序和筛选功能在客户端缓存。 排序功能的一个列中的值对记录进行排序。 筛选功能显示基于查找条件，同时完整记录的子集[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)维护在缓存中。 [重置](../../../ado/reference/rds-api/reset-method-rds.md)方法将执行条件并将替换当前**记录集**使用可更新**记录集**。  
  
 Null 值会导致出现类型不匹配错误。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [FilterColumn、 FilterCriterion、 FilterValue，SortColumn 和 SortDirection 属性和重置方法示例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 属性 (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterCriterion 属性 (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [SortColumn 属性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)






















