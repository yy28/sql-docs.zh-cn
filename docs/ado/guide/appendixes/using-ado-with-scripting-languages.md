---
title: "使用 ADO 的脚本语言 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7551fd26f6c0862115f0212777fb738a68e548a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="using-ado-with-scripting-languages"></a>使用 ADO 的脚本语言
在一个脚本编写环境 ADO 可以公开通过服务器端脚本的数据。 在此方案中，ADO，基础 OLE DB 提供程序，它使用，并引用给定的数据存储所需的任何其他组件安装在运行 Internet 信息服务 (IIS) 的服务器上。 使用 Active Server Pages (ASP)，ADO 是可以生成 HTML，例如脚本中引用的组件。 此 HTML 内容可以通过 HTTP 传递给客户端 Web 浏览器。 通过使用脚本，Web 页可以将操作发送回服务器端脚本，从而允许你更新、 遍历，或查看特定的数据。  
  
 在网页中使用 ActiveX 对象之前，务必知道对象是否是可安全执行脚本。 当对象被视为可安全执行脚本时，这意味着控件不能在用户的计算机上执行任何有害的操作，并因此可执行而不请求用户的批准。 下表列出的 ADO 对象，并指示它们是否可安全执行脚本。  
  
|Object|用于脚本编写的安全？|  
|------------|-------------------------|  
|ADO 连接|是|  
|ADO 命令|是|  
|ADO 参数|是|  
|ADO 记录集|是|  
|ADO 记录|是|  
|ADO 流|是|  
|ADO 错误|是|  
|ADOX 目录|是|  
|ADOX 单元集|是|  
|RDS DataControl|是|  
|RDS DataSpace|是|  
|RDS DataFactory|是|  
  
 下表列出了包含与 Windows DAC/MDAC 的提供程序，并指示它们是否可安全执行脚本。  
  
|提供程序|用于脚本编写的安全？|  
|--------------|-------------------------|  
|形状|是|  
|保留|是|  
|Remote|是|  
|OLE DB Provider for SQL Server (SQLOLEDB)|是|  
|OLE DB Provider for ODBC （msdasql） 一起使用|是|  
  
## <a name="odbc-data-sources"></a>ODBC 数据源  
 脚本和非脚本 ADO 代码之间的一个显著区别是 ODBC 数据源，如果使用。 对于非脚本应用程序，你可以在 ODBC 数据源管理器中创建用户 DSN。 对于在 IIS 下运行的脚本，你必须创建系统 DSN;否则你的脚本将无法识别你创建的数据源。 这适用于使用 Microsoft OLE DB 访问接口，对于通过 Microsoft IIS ODBC 任何 ADO 脚本应用程序。  
  
## <a name="referencing-the-ado-library"></a>引用 ADO 库  
 与脚本语言不适用。  
  
## <a name="handling-events"></a>处理事件  
 与脚本语言不适用。  
  
 以下主题包含有关中使用 ADO 的脚本语言的详细信息：  
  
-   [VBScript ADO 编程](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 编程](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft ActiveX 数据对象 (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [使用 ADO 与 Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [配合使用 ADO 与 Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
