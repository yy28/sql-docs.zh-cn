---
title: FilterCriterion 属性 (RDS) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60f66b1ff2fa7ad7424342da6b92e7d44d0e6444
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712702"
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion 属性 (RDS)
指示计算运算符筛选器值中使用。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *String*  
 一个**字符串**值，该值指定的计算运算符[FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)的记录。 可以为以下之一： <， \<=、 >、 > =、 =、 或 <>。  
  
## <a name="remarks"></a>备注  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， **FilterCriterion**，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)属性提供排序和筛选功能在客户端缓存。 排序功能的一个列中的值对记录进行排序。 筛选功能显示基于查找条件，同时完整记录的子集[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)维护在缓存中。 [重置](../../../ado/reference/rds-api/reset-method-rds.md)方法将执行条件并将替换当前**记录集**使用可更新**记录集**。  
  
 "！ ="运算符不能用于**FilterCriterion**; 相反，使用"<>"。  
  
 如果设置筛选器和排序属性并调用**重置**方法，首先筛选行集，然后对其进行排序。 升序排序，null 值，在顶部;对于降序排序，null 值，在底部 （升序是默认行为）。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [FilterColumn、 FilterCriterion、 FilterValue，SortColumn 和 SortDirection 属性和重置方法示例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 属性 (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue 属性 (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 属性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


