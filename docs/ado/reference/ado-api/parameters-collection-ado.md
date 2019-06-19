---
title: 参数集合 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a23b67141c7c07845438ed43f00d3124043a53c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704110"
---
# <a name="parameters-collection-ado"></a>参数集合 (ADO)
包含所有[参数](../../../ado/reference/ado-api/parameter-object.md)的对象[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
## <a name="remarks"></a>备注  
 一个**命令**对象具有**参数**组成的集合**参数**对象。  
  
 使用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)方法**命令**对象的**参数**集合检索提供程序的存储的过程或参数化的查询的参数信息中指定**命令**对象。 某些提供程序不支持存储的过程调用或参数化的查询;调用**刷新**方法**参数**集合使用此类提供程序时将返回错误。  
  
 如果你有未定义你自己**参数**对象中，访问**参数**集合，然后再调用**刷新**方法中，将自动调用 ADO方法和填充的集合。  
  
 可以调用提供程序来提高性能，如果知道参数的属性关联的存储过程或参数化查询你想要调用降到最低。 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法来创建**参数**具有相应的属性设置和使用的对象[追加](../../../ado/reference/ado-api/append-method-ado.md)方法将其添加到**参数**集合。 这样可以设置和返回参数值，而无需调用的参数信息的提供程序。 如果你正在编写不提供参数信息的提供程序，则必须手动填充**参数**使用此方法能够在所有使用参数的集合。 使用[删除](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)方法中删除**参数**中的对象**参数**集合，如有必要。  
  
 中的对象**参数**系列**记录集**转超出范围 （因此变得不可用） 时**记录集**已关闭。  
  
 在调用与存储的过程时**命令**，检索存储过程的返回值/输出参数，如下所示：  
  
1.  当调用存储的过程不会有任何参数，**刷新**方法**参数**调用之前，应调用集合**Execute**方法**命令**对象。  
  
2.  调用带有参数和显式追加到参数的存储的过程时**参数**具有集合**追加**，返回的值输出参数应追加到**参数**集合。 返回值必须先追加到**参数**集合。 使用**追加**添加到的其他参数**参数**按定义顺序的集合。 例如，存储的过程 SPWithParam 具有两个参数。 第一个参数， *InParam*，为输入的参数定义为以便您可以排除 (20)，而第二个参数*OutParam*，以便您可以排除 (20) 作为定义的输出参数。 可以使用以下代码返回的值输出参数来检索。  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  调用带有参数和通过调用配置的参数的存储的过程时**项**方法**参数**集合，该存储过程的返回值/输出参数可以从检索**参数**集合。 例如，存储的过程 SPWithParam 具有两个参数。 第一个参数， *InParam*，为输入的参数定义为以便您可以排除 (20)，而第二个参数*OutParam*，以便您可以排除 (20) 作为定义的输出参数。 可以使用以下代码返回的值输出参数来检索。  
  
    ```vb
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
  
## <a name="see-also"></a>请参阅  
 [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)
