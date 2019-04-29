---
title: ADO 错误参考 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a71b651df387bfe28992d426fd2080587e439ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063073"
---
# <a name="ado-errors"></a>ADO 错误
**ErrorValueEnum**常量介绍 ADO 错误值。 包括的值，这些枚举常量的完整列表请参阅[附录 b:ADO 错误](../../../ado/guide/appendixes/appendix-b-ado-errors.md)。 本部分将检查的一些更有趣的错误，并介绍它们，或若要解决此问题的解决方案可以引发某些特定情况。 这两个**ErrorValueEnum**列出了常量和简短的正十进制数。

|Number|ErrorValueEnum 常量|说明/可能的原因|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|提供程序无法执行请求的操作。|
|**3001**|**adErrInvalidArgument**|自变量的类型不正确、 不在可接受范围内，或与另一个冲突。 通常由一个 SQL SELECT 语句中的拼写错误导致此错误。 例如，拼写错误的字段名称或表名称可以生成此错误。 字段或 SELECT 语句中名为表中数据存储区不存在时，也可以发生此错误。|
|**3002**|**adErrOpeningFile**|无法打开文件。 指定一个拼写错误的文件名，或文件已被移动、 重命名或删除。 通过网络，这些驱动器可能会暂时不可用或网络流量可能会阻止连接。|
|**3003**|**adErrReadFile**|无法读取文件。 错误地指定的文件的名称，该文件可能被移动或删除，或该文件可能已损坏。|
|**3004**|**adErrWriteFile**|写入文件失败。 可能已经关闭文件，然后又试着将写入到它，或该文件可能已损坏。 如果该文件位于网络驱动器上，暂时性的网络状况可能会阻止写入到网络驱动器。|
|**3021**|**adErrNoCurrentRecord**|任一**BOF**或**EOF**为 True，或当前记录已被删除。 请求的操作需要当前记录。<br /><br /> 尝试通过使用更新的记录**查找**或**Seek**将记录指针移动到所需的记录。 如果未找到记录， **EOF**将为 True。 在出现故障后也会发生此错误**AddNew**或**删除**因为没有最新记录时这些方法都失败。|
|**3219**|**adErrIllegalOperation**|在此上下文中不允许操作。|
|**3220**|**adErrCantChangeProvider**|给定的提供程序不同于已在使用中。|
|**3246**|**adErrInTransaction**|**连接**对象不能在事务中显式关闭。 一个**记录集**或**连接**无法关闭当前参与事务的对象。 调用**RollbackTrans**或**CommitTrans**之前关闭对象。|
|**3251**|**adErrFeatureNotAvailable**|对象或提供程序不能执行请求的操作。 某些操作取决于特定的提供程序版本。|
|**3265**|**adErrItemNotFound**|不能在集合中找到项，对应于请求的名称或序号。 指定不正确的字段或表名称。|
|**3367**|**adErrObjectInCollection**|对象已在集合中。 无法追加。 对象无法添加到两次同一集合。|
|**3420**|**adErrObjectNotSet**|对象不再有效。|
|**3421**|**adErrDataConversion**|应用程序使用当前操作的错误类型的值。 您可能会提供操作需要一个流，例如的字符串。|
|**3704**|**adErrObjectClosed**|当对象已关闭时，不允许操作。 **连接**或**记录集**已关闭。 例如，一些其他例程可能会关闭全局对象。 可以通过检查来防止出现此错误**状态**尝试操作之前的属性。|
|**3705**|**adErrObjectOpen**|打开对象时，不允许操作。 无法打开处于打开状态的对象。 字段不能为打开追加**记录集**。|
|**3706**|**adErrProviderNotFound**|找不到提供程序。 它可能未正确安装。<br /><br /> 可能会错误地指定的提供程序名称、 指定的提供程序可能未安装计算机上正在执行你的代码，或安装可能已损坏。|
|**3707**|**adErrBoundToCommand**|**ActiveConnection**的属性**记录集**对象，具有**命令**对象作为其源，不能更改。 应用程序尝试分配一个新**连接**对象传递给**记录集**具有**命令**对象作为其源。|
|**3708**|**adErrInvalidParamInfo**|**参数**对象未正确定义。 提供的信息不一致或不完整。|
|**3709**|**adErrInvalidConnection**|不能使用连接来执行此操作。 它是已关闭或在此上下文中无效。|
|**3710**|**adErrNotReentrant**|无法处理事件时执行操作。 无法将导致再次触发的事件的事件处理程序中执行操作。 例如，导航方法不应调用内**WillMove**事件处理程序。|
|**3711**|**adErrStillExecuting**|以异步方式执行时，无法执行操作。|
|**3712**|**adErrOperationCancelled**|已由用户取消操作。 应用程序调用**CancelUpdate**或**CancelBatch**方法和当前操作已取消。|
|**3713**|**adErrStillConnecting**|以异步方式连接时，无法执行操作。|
|**3714**|**adErrInvalidTransaction**|协调事务无效，或尚未启动。|
|**3715**|**adErrNotExecuting**|不执行时，无法执行操作。|
|**3716**|**adErrUnsafeOperation**|在此计算机上的安全设置禁止访问其它域的数据源。|
|**3717**|**adWrnSecurityDialog**|仅限内部使用。 不要使用。 （而包括此项为完整起见。 此错误不应出现在你的代码。）|
|**3718**|**adWrnSecurityDialogHeader**|仅限内部使用。 不要使用。 （为了完整性而包括的项。 此错误不应出现在你的代码。）|
|**3719**|**adErrIntegrityViolation**|数据值与该字段的完整性约束冲突。 新的值**字段**会导致重复键。 一个值，窗体的两条记录之间的关系的一方可能无法更新。|
|**3720**|**adErrPermissionDenied**|没有足够的权限会阻止写入字段。 连接字符串中指定的用户没有适当的权限来写入**字段**。|
|**3721**|**adErrDataOverflow**|数据值为太大而无法表示字段数据类型。 分配为预期的字段太大的数字值。 例如，一个长整型值被赋予一个短整数字段。|
|**3722**|**adErrSchemaViolation**|数据值与数据类型或字段的约束冲突。 数据存储区具有不同的验证约束**字段**值。|
|**3723**|**adErrSignMismatch**|由于数据值带有符号而访问接口所使用的字段数据类型无符号转换失败。|
|**3724**|**adErrCantConvertvalue**|不能转换数据值，而原因并非符号不匹配或数据溢出。 例如，转换将截断数据。|
|**3725**|**adErrCantCreate**|数据值不能设置或检索，因为字段数据类型未知，或提供程序出现资源不足，无法执行该操作。|
|**3726**|**adErrColumnNotOnThisRow**|记录不包含此字段。 指定了不正确的字段名称或字段不在**字段**引用了当前记录的集合。|
|**3727**|**adErrURLDoesNotExist**|源 URL 或目标 URL 的父级不存在。 源或目标 URL 中没有犯了输入错误。 你可能`https://mysite/photo/myphoto.jpg`时实际上应具有`https://mysite/photos/myphoto.jpg`相反。 父 URL 中的输入错误 (在这种情况下，*照片*而不是*照片*) 导致该错误。|
|**3728**|**adErrTreePermissionDenied**|权限是不足以访问树或子树。 连接字符串中指定的用户没有适当的权限。|
|**3729**|**adErrInvalidURL**|URL 包含无效字符。 请确保键入的 URL 正确。 URL 采用注册到当前提供程序的方案 （例如，Internet 发布提供程序注册为 http）。|
|**3730**|**adErrResourceLocked**|指定 URL 表示的对象已由一个或多个其他进程锁定。 等待，直到该过程完成，然后重试该操作。 尝试访问的对象已由另一个用户或应用程序中的另一个进程锁定。 这是最有可能会出现在多用户环境中。|
|**3731**|**adErrResourceExists**|无法执行复制操作。 命名对象的目标 URL 已存在。 指定**adCopyOverwrite**替换对象。 如果未指定**adCopyOverwrite**复制文件时的目录中，当你尝试复制目标位置中已存在的项目时，复制会失败。|
|**3732**|**adErrCannotComplete**|服务器无法完成该操作。 这可能是因为服务器正忙于处理其他操作也可能是资源不足。|
|**3733**|**adErrVolumeNotFound**|提供程序找不到的 URL 所示的存储设备。 请确保键入的 URL 正确。 存储设备的 URL 可能不正确，但由于其他原因而可能发生此错误。 设备可能处于脱机状态或大量的网络流量可能会阻止从正在进行的连接。|
|**3734**|**adErrOutOfSpace**|无法执行操作。 提供程序无法获取足够的存储空间。 可能不会有足够的 RAM 或服务器上的临时文件的硬盘空间。|
|**3735**|**adErrResourceOutOfScope**|源或目标 URL 超出了当前记录的范围。|
|**3736**|**adErrUnavailable**|操作无法完成并且状态为不可用。 该字段可以是不可用或未尝试该操作。 另一个用户可能已更改或删除你尝试访问的字段。|
|**3737**|**adErrURLNamedRowDoesNotExist**|此 URL 通过名为记录不存在。 尝试打开文件使用时**记录**对象的文件名或文件的路径为拼写错误。|
|**3738**|**adErrDelResOutOfScope**|要删除对象的 URL 是超出了当前记录的范围。|
|**3747**|**adErrCatalogNotSet**|操作需要有效**ParentCatalog**。|
|**3748**|**adErrCantChangeConnection**|连接被拒绝。 所请求的新连接具有比已在使用一个不同的特征。|
|**3749**|**adErrFieldsUpdateFailed**|字段更新失败。 有关详细信息，检查**状态**单独的字段对象的属性。 在两种情况下会出现此错误： 在更改时**字段**过程中更改或添加记录到数据库，并更改的属性时的对象的值**字段**对象本身。<br /><br /> **记录**或**记录集**更新失败，因为其中一个当前记录中字段的问题。 枚举**字段**集合并检查**状态**属性的每个字段，以确定问题的原因。|
|**3750**|**adErrDenyNotSupported**|提供程序不支持共享的限制。 尝试限制文件共享和您的提供程序不支持这一概念。|
|**3751**|**adErrDenyTypeNotSupported**|提供程序不支持所请求的类型的共享限制。 尝试建立特定类型的文件共享您的提供程序不支持的限制。 请参阅提供程序的文档来确定支持哪些文件共享限制。|
