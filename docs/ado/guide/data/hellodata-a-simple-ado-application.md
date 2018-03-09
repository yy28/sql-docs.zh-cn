---
title: "HelloData： 一个简单的 ADO 应用程序 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 007f2842279607c722f6216d771751209ff723bc
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData： 一个简单的 ADO 应用程序
此简单的应用程序步骤通过每个四个主要的 ADO 操作： 获取、 检查、 编辑和更新数据。 对随附 Microsoft® SQL Server 的 Northwind 示例数据库执行这些操作。 若要专注于 ADO 的基础知识并避免出现代码混乱，该示例中的错误处理很小。  
  
### <a name="to-run-hellodata"></a>若要运行 HelloData  
  
1.  创建一个引用 ADO 库的新标准 EXE Visual Basic 项目。 有关详细信息，请参阅[引用 ADO 库](../../../ado/guide/referencing-the-ado-libraries.md)。  
  
2.  在窗体中，设置的顶部创建四个命令按钮**名称**和**标题**到本主题末尾的表中显示的值的属性。  
  
3.  在按钮的下面添加**Microsoft DataGrid 控件**(Msdatgrd.ocx)。 Msdatgrd.ocx 文件包含在 Visual Basic，并且位于 \windows\system32 或 \winnt\system32 目录中。 若要将 DataGrid 控件添加到 Visual Basic 工具箱窗格中，选择**组件...**从**项目**菜单。 然后旁边的复选框"Microsoft DataGrid 控件 6.0 (SP3) (OLEDB)"，然后单击**确定**。 若要将控件添加到项目中，将 DataGrid 控件从工具箱拖到 Visual Basic 窗体中。  
  
4.  创建**文本框中**网格下方的窗体上并设置其属性表中所示。 在完成时，格式应类似于下图。  
  
5.  最后，将复制中列出的代码[HelloData 代码](../../../ado/guide/data/hellodata-code.md)，并将它粘贴到代码编辑器窗口中的窗体。 按**F5**运行的代码。  
  
> [!NOTE]
>  在以下示例中，以及在指南中，用户 id"MyId"使用密码的"123abc 来向用于对服务器进行身份验证。 你应替换为你的服务器具有有效的登录凭据这些值。 此外，用替换的"MySQLServer"值与你的服务器的名称。  
  
 有关代码的详细说明，请参阅[对 HelloData 注释](../../../ado/guide/data/comments-on-hellodata.md)。  
  
 ![HelloData VB 应用程序显示 Form1](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|控件类型|属性|“值”|  
|------------------|--------------|-----------|  
|Form|名称|Form1|  
||高度|6500|  
||宽度|6500|  
|MS DataGrid|名称|grdDisplay1|  
|TextBox|名称|txtDisplay1|  
||多行|true|  
|命令按钮|名称|cmdGetData|  
||Caption|获取数据|  
|命令按钮|名称|cmdExamineData|  
||Caption|检查数据|  
|命令按钮|名称|cmdEditData|  
||Caption|编辑数据|  
|命令按钮|名称|cmdUpdateData|  
||Caption|更新数据|
