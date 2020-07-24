---
title: CreateRecordset 方法（RDS） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 53a391ccb25a32d628703543d95dc8e24668fcd5
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942489"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 方法 (RDS)
创建一个空的、断开连接的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>参数  
 *Object*  
 一个对象变量，它表示[RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)或[RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
 *ColumnsInfos*  
 特性的一个**变量**数组，用于定义创建的**记录集中**的每一列。 每个列定义都包含一个包含四个必需属性和一个可选属性的数组。  
  
|特性|说明|  
|---------------|-----------------|  
|名称|列标题的名称。|  
|类型|数据类型的整数。|  
|大小|字符宽度的整数，与数据类型无关。|  
|可空性|布尔值。|  
|Scale （可选）|此可选特性定义数值字段的小数位数。 如果未指定此值，数值将被截断为三个小数位数。 精度不受影响，但小数点后的位数将被截断为三。|  
  
 然后，将列数组集分组到一个数组中，该数组定义**记录集**。  
  
## <a name="remarks"></a>备注  
 服务器端业务对象可以使用非 OLE DB 的数据访问接口中的数据（例如包含股票行情的操作系统文件）来填充生成的**记录集**。  
  
 下表列出了**CreateRecordset**方法支持的[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。 列出的数字是用于定义字段的引用编号。  
  
 每个数据类型均为固定长度或可变长度。 应将固定长度类型定义为-1，因为大小是预先确定的，并且仍需要大小定义。 可变长度数据类型允许从1到32767的大小。  
  
 对于某些可变数据类型，可以将类型强制转换为替换列中所述的类型。 在创建并填充**记录集**之前，你将看不到替换项。 如果需要，可以检查实际数据类型。  
  
|长度|返回的常量|Number|替换|  
|------------|--------------|------------|------------------|  
|已修复|**adTinyInt**|16||  
|已修复|**adSmallInt**|2||  
|已修复|**adInteger**|3||  
|已修复|**adBigInt**|20||  
|已修复|**adUnsignedTinyInt**|17||  
|已修复|**adUnsignedSmallInt**|18||  
|已修复|**adUnsignedInt**|19||  
|已修复|**adUnsignedBigInt**|21||  
|已修复|**adSingle**|4||  
|已修复|**adDouble**|5||  
|已修复|**adCurrency**|6||  
|已修复|**adDecimal**|14||  
|已修复|**adNumeric**|131||  
|已修复|**adBoolean**|11||  
|已修复|**adError**|10||  
|已修复|**adGuid**|72||  
|已修复|**adDate**|7||  
|已修复|**adDBDate**|133||  
|已修复|**adDBTime**|134||  
|已修复|**adDBTimestamp**|135|7|  
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
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataFactory 对象 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [CreateRecordset 方法示例（VB）](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [CreateRecordset 方法示例（VBScript）](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)



