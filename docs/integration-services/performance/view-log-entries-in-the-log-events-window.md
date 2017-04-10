---
title: "在“日志事件”窗口中查看日志项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "日志 [Integration Services], 查看"
  - "Integration Services 包, 日志"
  - "包 [Integration Services], 日志"
ms.assetid: c02123c3-67fc-4370-ad14-91ed259f1873
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# 在“日志事件”窗口中查看日志项
  此过程描述如何运行包并查看它写入的日志项。 您可以实时查看日志项。 此外，还可以将写入 **“日志事件”** 窗口的日志项复制并保存，以便进行进一步分析。  
  
 不需要将日志项写入日志即可将这些项写入 **“日志事件”** 窗口。  
  
### 查看日志项  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在 **SSIS** 菜单上单击 **“日志事件”**。 通过将 View.LogEvents 命令映射为在 **“选项”** 对话框的 **“键盘”** 页中所选的组合键，您可以选择显示 **“日志事件”** 窗口。  
  
3.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
     当运行时遇到为日志记录启用的事件和自定义消息时，每个事件或消息的日志项将写入 **“日志事件”** 窗口。  
  
4.  在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
     日志项在 **“日志事件”** 窗口中保留可用状态，直到重新运行包、运行其他包或关闭 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
5.  在 **“日志事件”** 窗口中查看日志项。  
  
6.  （可选）单击要复制的日志项，右键单击，然后单击“复制”。  
  
7.  （可选）双击日志项，然后在“日志条目”对话框中，查看单个日志项的详细信息。  
  
8.  在 **“日志条目”** 对话框中，单击向上和向下键头，以显示上一个或下一个日志项，并单击复制图标以复制该日志项。  
  
9. 打开文本编辑器，粘贴，然后将日志项保存到文本文件中。  
  
## 另请参阅  
 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  