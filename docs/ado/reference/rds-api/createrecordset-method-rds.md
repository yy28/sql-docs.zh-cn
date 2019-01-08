---
title: CreateRecordset 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8646fba41809fe3ed6a062e7a066ed0dce5c007
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516720"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 方法 (RDS)
创建一个空断开[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parameters  
 *Object*  
 表示的对象变量[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)或[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *ColumnsInfos*  
 一个**Variant**的定义中的每列的属性数组**记录集**创建。 每个列定义中包含的四个必需的属性和一个可选属性的数组。  
  
|Attribute|Description|  
|---------------|-----------------|  
|“属性”|列标题的名称。|  
|类型|数据类型的整数。|  
|大小|以字符为单位，而不考虑数据类型为宽度的整数。|  
|可空性|布尔值。|  
|规模 （可选）|此可选属性定义的数值字段的小数位数。 如果未指定此值，数值将被截断为 3 的小数位数。 精度不受影响，但将为三个截断小数点后面的数字个数。|  
  
 列数组集然后分组到一个数组，它定义**记录集**。  
  
## <a name="remarks"></a>备注  
 服务器端业务对象可以填充得到**记录集**从非 OLE DB 数据访问接口的数据，如操作系统文件包含股票报价。  
  
 下表列出[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)支持的值为**CreateRecordset**方法。 列出的电话号码是用于定义字段的参考编号。  
  
 每种数据类型是固定的长度或可变长度。 固定长度的类型应定义大小为-1，因为大小是预先确定，仍然需要的大小定义。 长度可变的数据类型允许从 1 到 32767 之间的大小。  
  
 对于某些变量的数据类型，该类型可强制转换为替换列中记下的类型。 你将看不到之前的替换之后**记录集**创建并填充。 然后您可以检查实际的数据类型，如有必要。  
  
|长度|常量|Number|Substitution|  
|------------|--------------|------------|------------------|  
|固定|**adTinyInt**|16||  
|固定|**adSmallInt**|2||  
|固定|**adInteger**|3||  
|固定|**adBigInt**|20||  
|固定|**adUnsignedTinyInt**|17||  
|固定|**adUnsignedSmallInt**|18||  
|固定|**adUnsignedInt**|19||  
|固定|**adUnsignedBigInt**|21||  
|固定|**adSingle**|4||  
|固定|**adDouble**|5||  
|固定|**adCurrency**|6||  
|固定|**adDecimal**|14||  
|固定|**adNumeric**|131||  
|固定|**adBoolean**|11||  
|固定|**adError**|10||  
|固定|**adGuid**|72||  
|固定|**adDate**|7||  
|固定|**adDBDate**|133||  
|固定|**adDBTime**|134||  
|固定|**adDBTimestamp**|135|7|  
|变量|**adBSTR**|8|130|  
|变量|**adChar**|129|200|  
|变量|**adVarChar**|200||  
|变量|**adLongVarChar**|201|200|  
|变量|**adWChar**|130||  
|变量|**adVarWChar**|202|130|  
|变量|**adLongVarWChar**|203|130|  
|变量|**adBinary**|128||  
|变量|**adVarBinary**|204||  
|变量|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>请参阅  
 [CreateRecordset 方法示例 (VB)](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [CreateRecordset 方法示例 (VBScript)](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)



