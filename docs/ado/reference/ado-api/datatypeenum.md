---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7cb3e56d0219973be97b694ee2b22dbbb58eb0d8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698528"
---
# <a name="datatypeenum"></a>DataTypeEnum
指定的数据类型[字段](../../../ado/reference/ado-api/field-object.md)，[参数](../../../ado/reference/ado-api/parameter-object.md)，或[属性](../../../ado/reference/ado-api/property-object-ado.md)。 相应的 OLE DB 类型指示器显示在下表描述列中的括号中。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|与另一个数据类型常量，用于指示其他数据类型的数组始终结合使用标记值。 不适用于 ADOX。|  
|**adBigInt**|20|指示一个 8 字节有符号的整数 (DBTYPE_I8)。|  
|**adBinary**|128|指示一个二进制值 (DBTYPE_BYTES)。|  
|**adBoolean**|11|指示**布尔**值 (DBTYPE_BOOL)。|  
|**adBSTR**|8|指示一个以 null 结尾的字符串 (Unicode) (DBTYPE_BSTR)。|  
|**adChapter**|136|指示用于标识子行集 (DBTYPE_HCHAPTER) 中的行的一章将 4 字节值。|  
|**adChar**|129|指示一个字符串值 (DBTYPE_STR)。|  
|**adCurrency**|6|指示货币值 (DBTYPE_CY)。 带小数点右边的四个位数的定点数是货币。 它存储在按 10,000 缩放的 8 字节有符号整数。|  
|**adDate**|7|指示日期值 (DBTYPE_DATE)。 日期存储为双精度型，其整数部分是自 1899 年 12 月 30 日以来的天数数字的小数部分是一天的小部分。|  
|**adDBDate**|133|指示日期值 (yyyymmdd) (DBTYPE_DBDATE)。|  
|**adDBTime**|134|指示时间值 (hhmmss) (DBTYPE_DBTIME)。|  
|**adDBTimeStamp**|135|指示日期/时间戳 （yyyymmddhhmmss 加上在十亿分之一一小部分） (DBTYPE_DBTIMESTAMP)。|  
|**adDecimal**|14|指示具有固定的精度和小数位数 (DBTYPE_DECIMAL) 的精确数值。|  
|**adDouble**|5|指示一个双精度浮点值 (DBTYPE_R8)。|  
|**adEmpty**|0|未指定任何值 (DBTYPE_EMPTY)。|  
|**adError**|10|指示 32 位错误代码 (DBTYPE_ERROR)。|  
|**adFileTime**|64|指示表示从 1601 年 1 月 1 日 (DBTYPE_FILETIME) 起 100 纳秒间隔数的 64 位值。|  
|**adGUID**|72|指示全局唯一标识符 (GUID) (DBTYPE_GUID)。|  
|**adIDispatch**|9|指示一个指向**IDispatch** COM 对象 (DBTYPE_IDISPATCH) 上的接口。<br /><br /> **请注意**ADO 当前不支持此数据类型。 使用情况可能会导致不可预知的结果。|  
|**adInteger**|3|指示一个四字节有符号的整数 (DBTYPE_I4)。|  
|**adIUnknown**|13|指示一个指向**IUnknown** COM 对象 (DBTYPE_IUNKNOWN) 上的接口。<br /><br /> **请注意**ADO 当前不支持此数据类型。 使用情况可能会导致不可预知的结果。|  
|**adLongVarBinary**|205|指示长度的二进制值。|  
|**adLongVarChar**|201|指示一个长字符串值。|  
|**adLongVarWChar**|203|指示一个长时间的以 null 结尾的 Unicode 字符串值。|  
|**adNumeric**|131|指示具有固定的精度和小数位数 (DBTYPE_NUMERIC) 的精确数值。|  
|**adPropVariant**|138|指示自动化 PROPVARIANT (DBTYPE_PROP_VARIANT)。|  
|**adSingle**|4|指示一个单精度浮点值 (DBTYPE_R4)。|  
|**adSmallInt**|2|指示两个字节有符号的整数 (DBTYPE_I2)。|  
|**adTinyInt**|16|指示一个单字节有符号的整数 (DBTYPE_I1)。|  
|**adUnsignedBigInt**|21|指示一个 8 字节无符号的整数 (DBTYPE_UI8)。|  
|**adUnsignedInt**|19|指示一个四字节无符号的整数 (DBTYPE_UI4)。|  
|**adUnsignedSmallInt**|18|指示两个字节无符号的整数 (DBTYPE_UI2)。|  
|**adUnsignedTinyInt**|17|指示一个单字节无符号的整数 (DBTYPE_UI1)。|  
|**adUserDefined**|132|指示用户定义变量 (DBTYPE_UDT)。|  
|**adVarBinary**|204|指示一个二进制值。|  
|**adVarChar**|200|指示一个字符串值。|  
|**adVariant**|12|指示自动化**变体**(DBTYPE_VARIANT)。<br /><br /> **请注意**ADO 当前不支持此数据类型。 使用情况可能会导致不可预知的结果。|  
|**adVarNumeric**|139|指示数字值。|  
|**adVarWChar**|202|指示以 null 结尾的 Unicode 字符串。|  
|**adWChar**|130|指示 null 终止的 Unicode 字符字符串 (DBTYPE_WSTR)。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Type 属性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
