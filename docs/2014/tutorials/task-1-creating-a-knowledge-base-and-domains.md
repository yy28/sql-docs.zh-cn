---
title: 任务1：创建知识库和域 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f7ad3b085178c0d0cfe3ece010a571992e7fdb99
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064857"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>任务 1：创建知识库和域
  在此任务中，您将创建**供应商**知识库并创建用于清理数据和匹配数据的域以删除重复项。  
  
1.  启动**Data Quality Client**。 单击 "**开始**"，依次指向 "**所有程序**"、 **Microsoft SQL Server 2012**、" **Data Quality Services**"，然后单击 " **Data Quality Client**"。  
  
2.  在 "**连接到服务器**" 对话框中，选择安装 DQS 的数据库服务器实例，然后单击 "**连接**"。  
  
     !["连接到服务器" 对话框](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "“连接到服务器”对话框")  
  
3.  在 Data Quality Client 主页的 "**知识库管理**" 窗格中，单击 "**新建知识库**"。  
  
     ![知识库管理 - 新建知识库](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "知识库管理 - 新建知识库")  
  
4.  输入该知识库的**名称**的**供应商**。  
  
     ![新建知识库 - 域管理](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "新建知识库 - 域管理")  
  
5.  请确认将 "**创建知识库**" 字段设置为 "**无**"，因为您是从头开始创建**供应商**知识库的。  
  
6.  确认为**活动**选择了 "**域管理**"，然后单击 "**下一步**"。 通过域管理活动，您可以在知识库中创建和管理域。  
  
7.  在 "**域管理**" 窗口中，单击 "**创建域**" 工具栏按钮以创建域。  
  
     ![“创建域”工具栏按钮](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "“创建域”工具栏按钮")  
  
8.  在 "**创建域**" 对话框中，键入**域名**的 "**供应商 ID** "，然后单击 **"确定"**。  
  
     ![“创建域”对话框](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "“创建域”对话框")  
  
9. 重复执行前一步以便创建具有所有默认设置的以下域。 为简化本教程，请将所有域的**数据类型**设置为**String**。 其他允许的数据类型是：Integer、Decimal 和 Date。 如果选择了 "**使用前导值**" 选项（默认值），则会将所有同义词替换为输出中的同义词组的前导值。 设置**正常化字符串**选项（默认值）将删除域值中的任何特殊字符。 利用 "将**输出格式设置为**" 选项，您可以选择在输出域中的数据值时要应用的格式设置。 选择 "**启用拼写检查**器（默认值）" 可在填充域时对所有字符串值运行拼写检查器。 **语言**设置指定要应用的**拼写检查**器的语言版本。 选择 "**禁用语法错误算法**" 可填充域而不检查字符串值是否存在语法错误。 有关更多详细信息，请参阅 MSDN library 中的[创建域](https://msdn.microsoft.com/library/hh510401.aspx)主题。  
  
    -   Supplier Name  
  
    -   联系人电子邮件  
  
    -   Address Line  
  
    -   城市  
  
    -   状态  
  
    -   国家/地区  
  
    -   Zip  
  
## <a name="next-step"></a>下一步  
 [任务 2：手动添加域值](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
