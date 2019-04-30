---
title: 使用 ADO 与脚本语言 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fda0fb6446609a04178b533173a82bacc34c8cb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217753"
---
# <a name="using-ado-with-scripting-languages"></a>配合使用 ADO 与脚本语言
在脚本编写环境中，可使用 ADO 公开数据通过服务器端脚本。 在此方案中，ADO，基础 OLE DB 提供程序使用，并引用给定的数据存储区所需的任何其他组件安装在运行 Internet 信息服务 (IIS) 的服务器上。 ADO 使用 Active Server Pages (ASP)，是可以生成 HTML，例如脚本中引用的组件。 此 HTML 内容可以通过 HTTP 传递给客户端 Web 浏览器。 通过使用脚本，Web 页可以将操作发送回服务器端脚本，从而允许你更新、 遍历时，或查看特定的数据。  
  
 在网页中使用 ActiveX 对象之前，务必要知道的对象是否可安全执行脚本。 如果对象被视为可安全执行脚本，则意味着控件不能在用户计算机上执行任何有害操作，并因此可以执行而不请求用户的批准。 下表列出了 ADO 对象，并指示它们是否可安全执行脚本。  
  
|Object|用于编写脚本安全？|  
|------------|-------------------------|  
|ADO 连接|是|  
|ADO 命令|否|  
|ADO 参数|否|  
|ADO 记录集|是|  
|ADO 记录|是|  
|ADO Stream|是|  
|ADO 错误|否|  
|ADOX 目录|否|  
|ADOX 单元集|否|  
|RDS 数据控件|是|  
|RDS 数据空间|是|  
|RDS DataFactory|否|  
  
 下表列出了包括与 Windows DAC/MDAC 的提供程序，并指示它们是否可安全执行脚本。  
  
|提供程序|用于编写脚本安全？|  
|--------------|-------------------------|  
|形状|是|  
|持久保存|是|  
|Remote|是|  
|OLE DB Provider for SQL Server (SQLOLEDB)|否|  
|OLE DB Provider for ODBC (MSDASQL)|否|  
  
## <a name="odbc-data-sources"></a>ODBC 数据源  
 脚本编写和非脚本编写的 ADO 代码之间的一个显著区别是 ODBC 数据源时，如果使用。 对于非脚本编写的应用程序，可以创建一个用户 DSN 中 ODBC 数据源管理器。 对于在 IIS 下运行的脚本，您必须创建系统 DSN;否则脚本将无法识别创建的数据源。 这适用于使用 Microsoft OLE DB Provider for ODBC 通过 Microsoft IIS 任何 ADO 脚本应用程序。  
  
## <a name="referencing-the-ado-library"></a>引用 ADO 库  
 使用脚本语言不适用。  
  
## <a name="handling-events"></a>处理事件  
 使用脚本语言不适用。  
  
 以下主题包含有关使用 ADO 与脚本语言的更具体信息：  
  
-   [VBScript ADO 编程](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 编程](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft ActiveX 数据对象 (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [使用 ADO 与 Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [配合使用 ADO 与 Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
