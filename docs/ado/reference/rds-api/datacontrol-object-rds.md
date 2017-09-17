---
title: "DataControl 对象 (RDS) |Microsoft 文档"
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
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32e23b9cbd8cb74a43c6de48e006d4931835bcec
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="datacontrol-object-rds"></a>DataControl 对象 (RDS)
将绑定数据查询[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到一个或多个控件 （例如，文本框中，网格控件或组合框） 以显示**记录集**在网页上的数据。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>注释  
 类 ID **rds.DataControl**对象是 BD96C556-65A3-11 D 0 983A 00C04FC29E33。  
  
> [!NOTE]
>  如果收到错误[rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)或**rds.DataControl**对象不会加载，请确保你正在使用正确的类 id。 类已从版本 1.0 和 1.1 中更改这些对象的 Id。 另外，请注意使用时，必须设置甚至可以为 null 的列**RDS DataControl**对象。  
  
 你需要有关的基本方案，仅设置**SQL**，**连接**，和**服务器**属性**rds.DataControl**对象，将自动调用默认的业务对象，该对象[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)。  
  
 中的所有属性**rds.DataControl**是可选的因为自定义业务对象可以将替换为其功能。  
  
> [!NOTE]
>  如果为多个结果，请查询只显示前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)返回。 如果需要多个结果集，则为到其自身的每个分配**DataControl**。 为多个结果查询的示例可能包括：`"Select * from Authors, Select * from Topics"`  
  
 添加"DFMode = 20;"到连接字符串使用时**rds.DataControl**对象更新的数据时可以提高服务器的性能。 使用此设置，**提高**服务器上的对象使用的不太占用大量资源的模式。 但是，以下功能不可用在此配置：  
  
-   使用参数化的查询。  
  
-   获取之前调用的参数或列信息**执行**方法。  
  
-   设置**Transact 更新**到**True**。  
  
-   获取行状态。  
  
-   调用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法。  
  
-   通过刷新 （显式或自动）[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)属性。  
  
-   设置**命令**或[记录集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)属性。  
  
-   使用**adCmdTableDirect**。  
  
 **Rds.DataControl**对象的默认运行的异步模式。 如果你需要执行同步你的应用程序，设置[ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)参数等于**adcExecSync**和[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md)参数等于**adcFetchUpFront**，下面的示例中所示。  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 使用一个**rds.DataControl**要链接到一个或多个可视控件的单个查询的结果对象。 例如，假设代码例如名称、 居住、 出生位置、 年龄和优先级客户状态查询请求的客户数据。 你可以使用单个**rds.DataControl**对象在三个单独的文本框; 中显示客户的姓名、 年龄和区域复选框; 中的优先级客户状态和网格控件中的所有数据。  
  
 使用不同**rds.DataControl**对象链接到不同的可视控件的多个查询的结果。 例如，假设你使用一个查询，以获取有关客户的信息和另一个查询以获取有关客户已购买的商品的信息。 你想要在三个文本框和一个复选框和一个网格控件中的第二个查询的结果中显示的第一个查询结果。 如果你使用的默认业务对象 (**提高**)，你必须执行以下操作：  
  
-   添加两个**rds.DataControl**到 Web 页的对象。  
  
-   写入两个查询，每一个**SQL**这两个属性**rds.DataControl**对象。 一个**rds.DataControl**对象将包含 SQL 查询请求客户信息; 第二个将包含请求的客户已购买的商品列表的查询。  
  
-   在每个绑定的控件的对象标记中，指定要设置你想要在每个 visual 控件中显示的数据值的 DATAFLD 值。  
  
 数量没有计数限制**rds.DataControl**对象可以将嵌入在单个网页上使用对象标记。  
  
 在定义**rds.DataControl**对象在网页上，请使用非零**高度**和**宽度**值，例如 1 （以避免额外的空间包含）。  
  
 远程数据服务客户端组件尚的 Internet Explorer 4.0; 的一部分因此，不需要包括中的基本代码参数你**rds.DataControl**对象标记。  
  
 Internet Explorer 4.0 版或更高版本，可以通过使用 HTML 控件和 ActiveX® 控件，仅当它们标记为单元模型控件绑定到数据。  
  
> [!NOTE]
>  **Microsoft Visual Basic 用户** **rds.DataControl**为可安全执行脚本并且仅在基于 Web 的应用程序中使用。 Visual Basic 客户端应用程序具有它不需要。  
  
 本部分包含以下主题。  
  
-   [DataControl 对象 (RDS) 属性、 方法和事件](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataControl 对象示例 (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)























