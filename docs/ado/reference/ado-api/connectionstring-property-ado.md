---
title: ConnectionString 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01a930bc571e84c6ecfd38ce8415493c90ebd377
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828878"
---
# <a name="connectionstring-property-ado"></a>ConnectionString 属性 (ADO)
指示用来建立与数据源的连接的信息。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值。  
  
## <a name="remarks"></a>备注  
 使用**ConnectionString**属性来通过传递包含一系列的详细的连接字符串指定数据源*自变量* *= value*语句分隔分号。  
  
 ADO 支持五个参数为**ConnectionString**属性; 而无需任何处理通过 ADO 提供程序直接与任何其他参数传递。 参数 ADO 支持如下所示。  
  
|参数|Description|  
|--------------|-----------------|  
|*提供程序 =*|指定要用于连接的提供程序的名称。|  
|*文件名称 =*|指定的特定于提供程序的文件 （例如，持久化的数据源对象） 包含预设的连接信息的名称。|  
|*远程提供程序 =*|指定要打开客户端连接时使用的提供程序的名称。 （仅在远程数据服务中。）|  
|*远程服务器 =*|指定要打开客户端连接时使用的服务器的路径名称。 （仅在远程数据服务中。）|  
|*URL=*|连接字符串指定为标识资源，例如文件或目录的绝对 URL。|  
  
 在设置后**ConnectionString**属性并打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，该提供程序可能会通过将映射到 ADO 定义自变量名称等更改属性的内容及其特定提供程序的等效项。  
  
 **ConnectionString**属性将自动继承值，该值用于*ConnectionString*自变量[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，因此您可以重写当前**ConnectionString**属性期间**打开**方法调用。  
  
 因为*文件名*参数会使 ADO 来加载相关联的提供程序，则不能通过这两*提供程序*并*文件名*参数。  
  
 **ConnectionString**时该连接已关闭，只读方式打开时，属性为读/写。  
  
 中的自变量的副本**ConnectionString**属性将被忽略。 使用任何参数的最后一个实例。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**连接**对象， **ConnectionString**属性只能包含*远程提供程序*并*远程服务器*参数。  
  
 下表列出了每个 Windows 操作系统的默认 ADO 提供程序：  
  
|默认 ADO 提供程序|Windows 操作系统|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> （若要提高源代码的可读性，显式指定的提供程序名称的连接字符串中。）|Windows 2000 （32 位）<br /><br /> Windows XP （32 位）<br /><br /> Windows 2003 Server （32 位）<br /><br /> Windows Vista （32 位）<br /><br /> Windows Vista Service Pack 1 或更高版本 （32 位和 64 位）<br /><br /> Windows Vista （32 位和 64 位） 之后的 Windows 版本|  
|无默认值。<br /><br /> 当 ADO 应用程序在以下操作系统上运行，且未显式指定提供程序时，ADO 将返回以下错误:"ADODB。连接： 未指定提供程序和没有指定的默认提供程序"|Windows 2000 （64 位）<br /><br /> Windows XP （64 位）<br /><br /> Windows 2003 Server （64 位）<br /><br /> Windows Vista （64 位）|  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [ConnectionString、 ConnectionTimeout 和 State 属性示例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和 State 属性示例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
