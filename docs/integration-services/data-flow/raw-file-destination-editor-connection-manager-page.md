---
title: "原始文件目标编辑器（“连接管理器”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.rawfiledestinationconnectionmanager.f1"
ms.assetid: a0ec9643-3b44-4467-b855-f45ae4794f7f
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 原始文件目标编辑器（“连接管理器”页）
  使用原始文件目标编辑器配置原始文件目标以将原始数据写入文件。  
  
 **您希望做什么？**  
  
-   [打开原始文件目标编辑器](#open)  
  
-   [设置“连接管理器”选项卡上的选项](#connection)  
  
-   [设置“列”选项卡上的选项](#mapping)  
  
##  <a name="open"></a> 打开原始文件目标编辑器  
  
1.  将原始文件目标添加到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]包。  
  
2.  右键单击该组件，然后单击“编辑”。  
  
##  <a name="connection"></a> 设置“连接管理器”选项卡上的选项  
 **访问模式**  
 选择指定文件名的方式。 选择 **“文件名”** 可以直接输入文件名和路径，选择 **“变量中的文件名”** 可以指定包含文件名的变量。  
  
 “文件名”或“变量名称”  
 输入原始文件的名称和路径，或者选择包含文件名的变量。  
  
 **写入选项**  
 选择用来创建和写入文件的方法。  
  
 **生成初始原始文件**  
 单击此按钮可以生成仅包含列的空原始文件（仅元数据文件），而无需运行包。 该文件包含在 **“原始文件目标编辑器”** 的 **“列”**页上选择的列。 可以将原始文件源指向此仅元数据文件。  
  
 单击 **“生成初始原始文件”**时，将显示一个消息框。 单击 **“确定”** 可继续创建文件。 单击 **“取消”** 可选择 **“列”** 页上的其他列列表。  
  
##  <a name="mapping"></a> 设置“列”选项卡上的选项  
 **可用输入列**  
 选择要写入原始文件的一个或多个输入列。  
  
 **输入列**  
 在“可用输入列”下选择某一输入列时，该输入列将自动添加到此表中，或者，可直接在此表中选择该输入列。  
  
 **输出别名**  
 指定要用于输出列的备用名称。  
  
## 另请参阅  
 [原始文件目标](../../integration-services/data-flow/raw-file-destination.md)  
  
  