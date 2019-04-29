---
title: DataControl 对象 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa05b8b4be3c155c7ca59132892e0863dda60a5f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134411"
---
# <a name="datacontrol-object-rds"></a>DataControl 对象 (RDS)
将绑定数据查询[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到一个或多个控件 （例如，文本框中，网格控件或组合框） 以显示**记录集**Web 页上的数据。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>备注  
 类 ID **rds。DataControl**对象是 BD96C556-65A3-11 D 0 983A 00C04FC29E33。  
  
> [!NOTE]
>  如果收到错误[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)或**rds。DataControl**对象不会加载，请确保使用正确的类 id。 更改这些对象的 Id 已从版本 1.0 和 1.1 的类。 此外，请注意使用时，必须设置甚至可以为 null 的列**RDS DataControl**对象。  
  
 对于基本方案中，需要设置仅限**SQL**， **Connect**，并**服务器**的属性**rds。DataControl**对象，将自动调用默认业务对象，该对象[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)。  
  
 中的所有属性**rds。DataControl**是可选的因为自定义业务对象可以将替换为它们的功能。  
  
> [!NOTE]
>  如果为多个结果，查询仅在首[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)返回。 如果需要多个结果集，将分配到其自身的每个**DataControl**。 多个结果的查询的示例可能包括： `"Select * from Authors, Select * from Topics"`  
  
 添加"DFMode = 20;"到连接字符串使用时**rds。DataControl**更新数据时，对象可以提高服务器的性能。 使用此设置，**提高**对象在服务器上的使用较低占用大量资源的模式。 但是，以下功能不可用在此配置中：  
  
-   使用参数化的查询。  
  
-   获取参数或列的信息，然后再调用**Execute**方法。  
  
-   设置**Transact 更新**到**True**。  
  
-   获取行状态。  
  
-   调用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法。  
  
-   通过刷新 （显式或自动）[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)属性。  
  
-   设置**命令**或[记录集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)属性。  
  
-   使用**adCmdTableDirect**。  
  
 **Rds。DataControl**对象默认情况下在异步模式下运行。 如果你的应用需要执行同步，设置[ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)参数等于**adcExecSync**并[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md)参数等于**adcFetchUpFront**，如以下示例所示。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 使用一个**rds。DataControl**对象链接到一个或多个可视控件的单个查询的结果。 例如，假设代码如姓名、 居住、 出生地、 年龄和优先级客户状态查询请求的客户数据。 可以使用单个**rds。DataControl**对象以中三个单独的文本的框，显示客户的姓名、 年龄和区域复选框; 中的优先级客户状态和的 grid 控件中的所有数据。  
  
 使用不同**rds。DataControl**对象链接到不同的可视控件的多个查询的结果。 例如，假设您使用一个查询，以获取有关客户的信息以及用于获取有关客户已购买的商品的信息的第二个查询。 你想要显示三个文本框和一个复选框和一个网格控件中的第二个查询的结果中的第一个查询的结果。 如果您使用默认的业务对象 (**提高**)，必须执行以下操作：  
  
-   添加两个**rds。DataControl**到 Web 页的对象。  
  
-   写入两个查询，每个**SQL**这两个属性**rds。DataControl**对象。 一个**rds。DataControl**对象将包含请求的客户信息的 SQL 查询; 第二个将包含请求的客户已购买的商品列表的查询。  
  
-   在每个绑定的控件的对象标记，指定要设置你想要在每个可视控件中显示的数据值的 DATAFLD 值。  
  
 数量没有计数限制**rds。DataControl**对象，您可以通过在单个网页上使用对象标记中嵌入。  
  
 在定义**rds。DataControl**对象在网页上，请使用非零**高度**并**宽度**值，例如 1 （以避免包含额外的空间）。  
  
 远程数据服务客户端组件已作为 Internet Explorer 4.0; 的一部分因此，不需要包括中的基本代码参数在**rds。DataControl**对象标记。  
  
 Internet Explorer 4.0 或更高版本，可以通过使用 HTML 控件和 ActiveX® 控件，仅当它们标记为单元模型控件绑定到数据。  
  
> [!NOTE]
>  **Microsoft Visual Basic 用户** **rds。DataControl**脚本是安全的和仅在基于 Web 的应用程序中使用。 Visual Basic 客户端应用程序不需要它。  
  
 本部分包含以下主题。  
  
-   [DataControl 对象 (RDS) 属性、方法和事件](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [DataControl 对象示例 (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















