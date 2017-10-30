---
title: "在自定义应用程序中使用 RSClientPrint 控件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 57312a2c4c75a9df1abc55baa833772c9949270c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>在自定义应用程序中使用 RSClientPrint 控件
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX 控件， **RSPrintClient**，提供在 HTML 查看器中查看报表的客户端打印。 它提供了**打印**对话框中，以便用户可以启动打印作业、 预览报表，指定要打印的页和更改边距。 在客户端打印操作过程中，报表服务器通过图像 (EMF) 呈现扩展插件呈现报表，使用操作系统的打印功能创建打印作业并将作业发送到打印机。  
  
 通过客户端打印功能，可以避开用户计算机上的浏览器打印设置，改用报表的页面尺寸、边距、表头文本和表尾文本来创建打印输出，从而控制和提高 HTML 报表的打印输出质量。 该打印控件通过读取报表的属性值来设置页大小和边距。  
  
 开发人员想要启用第三方工具栏或查看器中的客户端打印功能可以访问通过 ActiveX 控件**RSClientPrint** COM 对象。 该控件可以自由分发。 下表列出了使用该控件的建议：  
  
-   使用该控件提高基于 Web 的报表的打印质量。 你可以在任何指定对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-兼容的编程语言或脚本中。 该控件不用于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 窗体应用程序。  
  
-   从 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 程序文件复制 .cab 文件，并将其添加到自定义应用程序基本代码中。  
  
-   使用\<对象 > 标记来指定的控件。  
  
-   在 OBJECT CODEBASE 属性中为 .cab 文件指定相对 URL 或完全限定的 URL。  
  
-   为 .cab 文件指定您自己的应用程序版本信息，以跟踪在您的应用程序中使用的版本。  
  
-   查阅有关图像 (EMF) 呈现的联机丛书主题，以了解如何呈现页面以供打印预览和输出。  
  
## <a name="rsprintclient-overview"></a>RSPrintClient 概述  
 该控件显示一个自定义打印对话框，它支持其他打印对话框常见的功能，包括打印预览、指定特定页和范围的页面选择、页边距和打印方向等功能。 该控件打包为 CAB 文件。 中的文本**打印**对话框本地化为所有中支持的语言[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 **RSPrintClient** ActiveX 控件使用图像呈现扩展插件 (EMF) 来打印报表。 使用的 EMF 设备信息包括：StartPage、EndPage、MarginBottom、MarginLeft、MarginTop、MarginRight、PageHeight 和 PageWidth。 不支持图像呈现的其他设备信息设置。  
  
### <a name="language-support"></a>语言支持  
 该打印控件可以提供不同语言的用户界面文本，接受符合不同度量系统标准的输入值。 使用的语言和测量系统由**区域性**和**UICulture**属性。 这两个属性都接受 LCID 值。 如果为所支持语言的变体语言指定 LCID，则会应用最接近的匹配语言。 如果不支持指定的 LCID，并且没有最接近的匹配 LCID，则会应用英语（美国）。  
  
## <a name="using-rsclientprint-in-code"></a>在代码中使用 RSClientPrint  
 **RSClientPrint**对象用来以编程方式向 ActiveX 控件和其方法和属性的访问。 该控件为打印预览提供了一个模式对话框。  
  
### <a name="specifying-default-values"></a>指定默认值  
 可以初始化**打印**对话框使用页边距和页面的值的报表。 默认情况下，**打印**对话框中初始化报表定义中的值。 您可以使用这些默认值，也可以通过设置对象属性来指定不同的值。  
  
 所有尺寸都是以毫米为单位进行设置的。 度量转换发生在运行时，如果**区域性**和**UICulture**设置为不使用公制的区域设置。  
  
 若要了解哪些值用于页尺寸和边距，可以使用**GetProperties**方法来检索默认值：  
  
-   **PageHeight**和**PageWidth**指定的默认页面高度和宽度。 在启动该打印控件时，将使用这些属性值选择可用于当前所选打印机的最接近的纸张大小。 如果**PageWidth**非常比**PageHeight**，将方向设置为横向。 否则，方向设置为“纵向”。  
  
-   **LeftMargin**， **RightMargin**， **TopMargin**，和**文本底边距**都设置为默认情况下 12.2 毫米等。  
  
 这些属性存储在**项**报表服务器上的属性集合。 每次更新报表定义时，都将覆盖这些值。  
  
### <a name="rsclientprint-properties"></a>RSClientPrint 属性  
  
|属性|类型|RW|默认|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|双精度|RW|报表设置|获取或设置左边距。 如果开发人员没有设置或报表中未指定，则默认值为 12.2 毫米。|  
|MarginRight|双精度|RW|报表设置|获取或设置右边距。 如果开发人员没有设置或报表中未指定，则默认值为 12.2 毫米。|  
|MarginTop|双精度|RW|报表设置|获取或设置上边距。 如果开发人员没有设置或报表中未指定，则默认值为 12.2 毫米。|  
|MarginBottom|双精度|RW|报表设置|获取或设置下边距。 如果开发人员没有设置或报表中未指定，则默认值为 12.2 毫米。|  
|PageWidth|双精度|RW|报表设置|获取或设置页宽。 如果未设置由开发人员或报表定义默认值为 215.9 毫米等。|  
|PageHeight|双精度|RW|报表设置|获取或设置页高。 如果开发人员或报表定义中未进行设置，则默认值为 279.4 毫米。|  
|Culture|Int32|RW|浏览器区域设置|指定区域设置标识符 (LCID)。 此值将确定用户输入的度量单位。 例如，如果用户键入**3**，值将测量以毫米为单位，如果语言为法语或英寸如果语言是英语 （美国）。 有效值包括：1028、1031、1033、1036、1040、1041、1042、2052、3082。|  
|UICulture|字符串|RW|客户端区域性|指定对话框字符串的本地化语言。 “打印”对话框中的文本已本地化为以下语言：简体中文、繁体中文、英语、法语、德语、意大利语、日语、朝鲜语和西班牙语。 有效值包括：1028、1031、1033、1036、1040、1041、1042、2052、3082。|  
|Authenticate|Boolean|RW|False|指定控件是否向报表服务器发出 GET 命令，以启动无会话打印连接。|  
  
### <a name="when-to-set-the-authenticate-property"></a>何时设置 Authenticate 属性  
 通过打印时在浏览器会话中，不需要设置**进行身份验证**属性。 在活动会话的上下文中，打印控件对报表服务器的所有请求都是通过浏览器来处理的。 浏览器会设置与报表服务器通信所需的会话变量。  
  
 如果打印出的会话 （例如，无需先打开它直接向打印机发送报表） 时，使用打印控件必须发出 HTTP**获取**设置与报表服务器的会话的请求。 颁发**获取**请求，你将设置**进行身份验证**到**True**。  
  
 你只需以发出**获取**请求，如果你使用 Windows 集成安全性或基本身份验证。 如果你使用的 forms 身份验证，**进行身份验证**忽略属性。 此时，应用程序代码必须使用您提供的自定义安全扩展插件来设置会话及验证用户身份。 如果使用窗体身份验证，请确保针对身份验证 cookie 设置的过期值可使会话保留一段合理的时间。 如果该值过低，每当 cookie 过期时，系统都将提示用户提供登录凭据。  
  
### <a name="clsids"></a>Clsid  
 当在内部运行报表时，使用以下 CLSID 值。  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 当在 Windows Azure SQL Reporting 中运行报表时，使用以下 CLSID 值。  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>RSPrintClient 对 Print 方法的支持  
 **RSClientPrint**对象支持**打印**以启动打印对话框中的方法。 **打印**方法具有以下参数。  
  
|参数|I/O|类型|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|In|字符串|指定报表服务器虚拟目录 (例如， `https://adventure-works/reportserver`)。|  
|ReportPathParameters|In|字符串|指定报表在报表服务器文件夹命名空间中的全名，包括参数。 对报表的检索是通过 URL 访问进行的。 例如：“/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234”。|  
|ReportName|In|字符串|报表的简称（在上面的示例中，简称为 Employee Sales Summary）。 它显示在“打印”对话框和打印队列中。|  
  
### <a name="example"></a>示例  
 下面的 HTML 示例演示如何指定.cab 文件中，**打印**方法，并在 JavaScript 中的属性：  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>另請參閱  
 [从使用打印控件 &#40; 浏览器中打印报表报表生成器和 SSRS &#41;](../../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [打印报表 &#40;报表生成器和 SSRS &#41;](../../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [图像设备信息设置](../../../reporting-services/image-device-information-settings.md)  
  
  

