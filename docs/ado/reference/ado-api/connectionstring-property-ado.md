---
title: "ConnectionString 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34db69d25ff835de4f8c81d252c99017ae4acbb5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connectionstring-property-ado"></a>ConnectionString 属性 (ADO)
指示用于建立与数据源的连接的信息。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值。  
  
## <a name="remarks"></a>注释  
 使用**ConnectionString**属性通过传递包含一系列连接的详细信息字符串中指定数据源*参数* *= value*语句隔开分号。  
  
 ADO 支持五个参数**ConnectionString**属性; 任何其他自变量传入直接与提供程序，没有通过 ADO 任何处理。 自变量 ADO 支持如下所示。  
  
|参数|Description|  
|--------------|-----------------|  
|*提供程序 =*|指定要用于连接提供程序的名称。|  
|*文件名称 =*|指定的提供程序特定文件 （例如，持久化的数据源对象） 包含预设的连接信息的名称。|  
|*远程提供程序 =*|指定要在打开的客户端连接时使用的提供程序的名称。 （仅限在远程数据服务中。）|  
|*远程服务器 =*|指定要在打开的客户端连接时使用的服务器的路径名称。 （仅限在远程数据服务中。）|  
|*URL =*|连接字符串指定为标识某个资源，例如文件或目录的绝对 URL。|  
  
 设置之后**ConnectionString**属性，然后打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，该提供程序可能例如，更改属性，此内容，通过将映射到的 ADO 定义自变量名称及其特定的提供程序的等效项。  
  
 **ConnectionString**属性都将自动继承的值用于*ConnectionString*参数[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法，因此你可以重写当前**ConnectionString**期间属性**打开**方法调用。  
  
 因为*文件名*自变量会使 ADO 加载相关联的提供程序，都不能传递*提供程序*和*文件名*自变量。  
  
 **ConnectionString**属性为读/写，当连接已关闭，并且只读打开时。  
  
 中的自变量的重复项**ConnectionString**属性将被忽略。 使用任何自变量的最后一个实例。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**连接**对象， **ConnectionString**属性只能包含*远程提供程序*和*远程服务器*参数。  
  
 下表列出了每个 Windows 操作系统的系统默认 ADO 提供程序：  
  
|默认 ADO 提供程序|Windows 操作系统|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> （若要提高代码的源代码的可读性，显式指定的提供程序名称在连接字符串中。）|Windows 2000 （32 位）<br /><br /> Windows XP （32 位）<br /><br /> Windows 2003 Server （32 位）<br /><br /> Windows Vista （32 位）<br /><br /> Windows Vista Service Pack 1 或更高版本 （32 位和 64 位）<br /><br /> Windows Vista （32 位和 64 位） 后的 Windows 版本|  
|无默认值。<br /><br /> 如果 ADO 应用程序在以下操作系统上运行，并且未显式指定提供程序，ADO 将返回以下错误:"ADODB。连接： 未指定提供程序和没有指定的默认提供程序"|Windows 2000 （64 位）<br /><br /> Windows XP （64 位）<br /><br /> Windows 2003 Server （64 位）<br /><br /> Windows Vista （64 位）|  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ConnectionString、 ConnectionTimeout，以及状态属性示例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和状态属性示例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)

