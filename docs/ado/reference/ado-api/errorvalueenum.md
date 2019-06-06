---
title: ErrorValueEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f9efa743e6e5f9efe99e08001980ab87bf13247
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695223"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
指定 ADO 运行时错误的类型。  
  
 列出了三种形式的错误号：  
  
-   正小数低两个字节的十进制格式的完整编号。 此号码在默认 Visual Basic 错误消息对话框中显示。 例如，运行时的错误"3707"。  
  
-   完整的错误号的负小数十进制转换。  
  
-   完整的错误号的十六进制十六进制表示形式。 Windows 设备代码为第四个数字。 ADO 错误号的设施代码*A*。例如：0x800***A***0E7B.  
  
> [!NOTE]
>  OLE DB 错误可能会传递到 ADO 应用程序。 通常情况下，可以通过的 Windows 设备代码标识这些*4*。 例如，0x800***4***。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707 -2146824581 0x800A0E7B|不能更改**ActiveConnection**的属性**记录集**对象，它具有**命令**对象作为其源。|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|服务器无法完成该操作。|  
|**adErrCantChangeConnection**|3748 -2146824540 0x800A0EA4|连接被拒绝。 所请求的新连接具有比已在使用不同的特征。|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|提供的提供程序不同于已被使用。|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|不能转换数据值，而原因并非符号不匹配或数据溢出。 例如，转换将截断数据。|  
|**adErrCantCreate**|3725 -2146824563 0x800A0E8D|数据值不能设置或检索，因为字段数据类型未知，或提供程序出现资源不足，无法执行该操作。|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|操作需要有效**ParentCatalog**。|  
|**adErrColumnNotOnThisRow**|3726 -2146824562 0x800A0E8E|记录不包含此字段。|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|应用程序使用当前操作的错误类型的值。|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|数据值为太大而无法表示字段数据类型。|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|要删除的 URL 是对象的超出了当前记录的范围。|  
|**adErrDenyNotSupported**|3750 -2146824538 0x800A0EA6|提供程序不支持共享的限制。|  
|**adErrDenyTypeNotSupported**|3751 -2146824537 0x800A0EA7|提供程序不支持所请求的类型的共享限制。|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|对象或提供程序不能执行请求的操作。|  
|**adErrFieldsUpdateFailed**|3749 -2146824539 0x800A0EA5|字段更新失败。 有关详细信息，检查**状态**单独的字段对象的属性。|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|在此上下文中不允许操作。|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|数据值与该字段的完整性约束冲突。|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**连接**对象不能在事务中显式关闭。|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|自变量的类型不正确、 不在可接受范围内，或与另一个冲突。|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|不能使用连接来执行此操作。 它是已关闭或在此上下文中无效。|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**参数**对象未正确定义。 提供的信息不一致或不完整。|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|协调事务无效，或尚未启动。|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|URL 包含无效字符。 请确保键入的 URL 正确。|  
|**adErrItemNotFound**|3265 -2146825023 0x800A0CC1|对应到请求的名称或序号的集合中找不到项。|  
|**adErrNoCurrentRecord**|3021 -2146825267 0x800A0BCD|任一**BOF**或**EOF**为 True，或当前记录已被删除。 请求的操作需要当前记录。|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|不执行时，无法执行操作。|  
|**adErrNotReentrant**|3710 -2146824578 0x800A0E7E|无法处理事件时执行操作。|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|当对象已关闭时，不允许操作。|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|对象已在集合中。 无法追加。|  
|**adErrObjectNotSet**|3420 -2146824868 0x800A0D5C|对象不再有效。|  
|**adErrObjectOpen**|3705 -2146824583 0x800A0E79|打开对象时，不允许操作。|  
|**adErrOpeningFile**|3002 -2146825286 0x800A0BBA|无法打开文件。|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|已由用户取消操作。|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|无法执行操作。 提供程序无法获取足够的存储空间。|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|没有足够的权限会阻止写入字段。|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|提供程序没有执行所请求的操作。|  
|**adErrProviderNotFound**|3706 -2146824582 0x800A0E7A|找不到提供程序。 它可能未正确安装。|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|无法读取文件。|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|无法执行复制操作。 命名对象的目标 URL 已存在。 指定**adCopyOverwrite**替换对象。|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|指定 URL 表示的对象已由一个或多个其他进程锁定。 等待，直到该过程完成，然后重试该操作。|  
|**adErrResourceOutOfScope**|3735 -2146824553 0x800A0E97|源或目标 URL 超出了当前记录的范围。|  
|**adErrSchemaViolation**|3722 -2146824566 0x800A0E8A|数据值与数据类型或字段的约束冲突。|  
|**adErrSignMismatch**|3723 -2146824565 0x800A0E8B|由于数据值带有符号而访问接口所使用的字段数据类型无符号转换失败。|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|以异步方式连接时，无法执行操作。|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|以异步方式执行时，无法执行操作。|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|权限是不足以访问树或子树。|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|操作未完成并且状态为不可用。 该字段可以是不可用或未尝试该操作。|  
|**adErrUnsafeOperation**|3716 -2146824572 0x800A0E84|此计算机上的安全设置阻止访问另一个域上的数据源。|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|源 URL 或目标 URL 的父级不存在。|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|此 URL 通过名为记录不存在。|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|提供程序找不到的 URL 所示的存储设备。 请确保键入的 URL 正确。|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|写入文件失败。|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|仅限内部使用。 请勿使用。|  
|**adWrnSecurityDialogHeader**|3718 -2146824570 0x800A0E86|仅限内部使用。 请勿使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
 只有 ADO/WFC 等效项的以下子集进行定义。  
  
|常量|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>适用范围  
 [Number 属性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [ADO 错误代码](../../../ado/guide/appendixes/ado-error-codes.md)
