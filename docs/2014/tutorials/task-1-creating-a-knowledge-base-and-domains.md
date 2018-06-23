---
title: 任务 1： 创建知识库和域 |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: beec636f9137802c6651f0c08889acf73000b063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125950"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>任务 1：创建知识库和域
  在此任务中，你将创建**供应商**知识库并创建清理数据和数据相匹配的情况下用于删除重复项的域。  
  
1.  启动**数据质量客户端**。 单击**启动**，指向**所有程序**，单击**Microsoft SQL Server 2012**，单击**Data Quality Services**，然后单击**数据质量客户端**。  
  
2.  在**连接到服务器**对话框框中，选择数据库服务器实例的 DQS 安装，且单击**连接**。  
  
     ![连接到服务器对话框](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "连接到服务器对话框")  
  
3.  在数据质量客户端主页上，在**知识库管理**窗格中，单击**新知识库**。  
  
     ![知识库管理-新 KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "知识库管理-新 KB")  
  
4.  输入**供应商**为**名称**知识库。  
  
     ![新的知识库的域管理](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "新知识库的域管理")  
  
5.  确认**从创建知识库**字段设置为**无**由于您正在创建**供应商**从零开始的知识库。  
  
6.  确认**域管理**为选择**活动**单击**下一步**。 通过域管理活动，您可以在知识库中创建和管理域。  
  
7.  在**域管理**窗口中，单击**创建域**工具栏按钮，以创建域。  
  
     ![创建域工具栏按钮](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "创建域工具栏按钮")  
  
8.  在**创建域**对话框中，键入**供应商 ID**为**域名**，然后单击**确定**。  
  
     ![创建域对话框](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "创建域对话框")  
  
9. 重复执行前一步以便创建具有所有默认设置的以下域。 为了简化本教程，你可以设置**数据类型**的选定内容的所有域作为**字符串**。 其他允许的数据类型是：Integer、Decimal 和 Date。 当**使用前导值**选项是选中状态 （默认），所有同义词都替换在输出中的同义词组的前导值。 设置**规范化字符串**选项 （默认值） 中删除域值中的任何特殊字符。 **输出格式设置为**选项，可以选择在域中的数据值输出时采用的格式。 选择**启用拼写检查器**（默认值） 填充域时对所有字符串值运行拼写检查器。 **语言**设置指定的语言版本**拼写检查器**你想要应用。 选择**禁用语法错误算法**可填充域而不会检查是否存在语法错误的字符串值。 请参阅[创建域](http://msdn.microsoft.com/library/hh510401.aspx)更多详细信息的 MSDN 库中的主题。  
  
    -   Supplier Name  
  
    -   Contact Email  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   Country  
  
    -   Zip  
  
## <a name="next-step"></a>下一步  
 [任务 2：手动添加域值](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  