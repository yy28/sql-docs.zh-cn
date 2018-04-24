---
title: 参数集合 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e6557489b5051a7d92864b662b1822b9e6d0dff4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="parameters-collection-ado"></a>参数集合 (ADO)
包含所有[参数](../../../ado/reference/ado-api/parameter-object.md)的对象[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
## <a name="remarks"></a>注释  
 A**命令**对象具有**参数**组成的集合**参数**对象。  
  
 使用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法**命令**对象的**参数**集合检索提供程序的存储的过程或参数化的查询的参数信息指定在**命令**对象。 某些提供程序不支持存储的过程调用或参数化的查询;调用**刷新**方法**参数**集合时使用此类提供程序将返回错误。  
  
 如果你具有未定义你自己**参数**对象，并且您访问**参数**集合，然后再调用**刷新**方法时，将自动调用 ADO方法并填充你的集合。  
  
 你可以尽量减少对的调用提供程序来提高性能，如果你知道的参数的属性与存储过程或参数化查询你想要调用。 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法来创建**参数**相应的属性设置和使用的对象[追加](../../../ado/reference/ado-api/append-method-ado.md)方法以将其添加到**参数**集合。 这样就可以设置和返回参数值，而无需调用该提供程序的参数信息。 如果要写入的提供程序未提供参数信息，则必须手动填充**参数**使用此方法要能够使用参数的集合。 使用[删除](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)方法移除**参数**对象从**参数**集合，如有必要。  
  
 中的对象**参数**集合**记录集**转超出范围 （因此变得不可用） 时**记录集**已关闭。  
  
 在调用与存储的过程时**命令**，存储过程返回的值输出参数检索，如下所示：  
  
1.  当调用存储的过程不具有任何参数，**刷新**方法**参数**集合应该调用，然后再调**执行**方法**命令**对象。  
  
2.  在调用带有参数和显式追加参数传递给存储的过程时**参数**具有集合**追加**，应将返回的值输出参数追加到**参数**集合。 返回值必须首先追加到**参数**集合。 使用**追加**以添加其他参数到**参数**顺序定义的集合。 例如，存储的过程 SPWithParam 具有两个参数。 第一个参数， *InParam*，是定义为以便您可以排除 (20) 的输入的参数和第二个参数， *OutParam*，是定义以便您可以排除 (20) 为一个输出参数。 你可以检索返回值/输出参数替换为以下代码。  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOuput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  在调用带有参数和配置参数调用存储的过程时**项**方法**参数**集合，返回的值输出参数的存储过程可以从检索**参数**集合。 例如，存储的过程 SPWithParam 具有两个参数。 第一个参数， *InParam*，是定义为以便您可以排除 (20) 的输入的参数和第二个参数， *OutParam*，是定义以便您可以排除 (20) 为一个输出参数。 你可以检索返回值/输出参数替换为以下代码。  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 本部分包含以下主题。  
  
-   [参数集合属性、 方法和事件](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)
