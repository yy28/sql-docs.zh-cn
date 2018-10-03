---
title: 任务 1： 创建知识库和域 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1222d6d217c004790336a6a234d7f52154e148ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132429"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>任务 1：创建知识库和域
  在本任务中，您将创建**供应商**知识库，并创建用于清理数据和匹配数据以便删除重复项的域。  
  
1.  启动**数据质量客户端**。 单击**启动**，依次指向**所有程序**，单击**Microsoft SQL Server 2012**，单击**Data Quality Services**，然后单击**数据质量客户端**。  
  
2.  在中**连接到服务器**对话框框中，选择数据库服务器实例依据 DQS 安装，并单击**Connect**。  
  
     ![连接到服务器对话框](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "连接到服务器对话框")  
  
3.  在数据质量客户端主页上，在**知识库管理**窗格中，单击**新的知识库**。  
  
     ![知识库管理-新建知识库](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "知识库管理-新建知识库")  
  
4.  输入**供应商**有关**名称**知识库。  
  
     ![新建知识库-域管理](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "新建知识库-域管理")  
  
5.  确认**从创建知识库**字段设置为**None**由于您创建的**供应商**从零开始的知识库。  
  
6.  确认**域管理**选择了**活动**然后单击**下一步**。 通过域管理活动，您可以在知识库中创建和管理域。  
  
7.  在中**域管理**窗口中，单击**创建域**工具栏按钮以创建一个域。  
  
     ![创建域工具栏按钮](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "创建域工具栏按钮")  
  
8.  中**创建一个域**对话框中，键入**Supplier ID**有关**域名**，然后单击**确定**。  
  
     ![创建域对话框](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "创建域对话框")  
  
9. 重复执行前一步以便创建具有所有默认设置的以下域。 若要简化本教程，请设置**数据类型**的所有域作为**字符串**。 其他允许的数据类型是：Integer、Decimal 和 Date。 当**使用前导值**选项是所选 （默认值），所有同义词将都替换为输出中同义词组的前导值。 设置**规范化字符串**选项 （默认值） 在域值中删除任何特殊字符。 **输出格式设置为**选项允许您选择的域中的数据值输出时采用的格式设置。 选择**启用拼写检查器**（默认值） 可填充域时对所有的字符串值运行拼写检查器。 **语言**设置指定的语言版本**拼写检查器**你想要应用。 选择**禁用语法错误算法**可填充域而不检查是否存在语法错误的字符串值。 请参阅[创建一个域](http://msdn.microsoft.com/library/hh510401.aspx)更多详细信息的 MSDN library 中的主题。  
  
    -   Supplier Name  
  
    -   Contact Email  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   Country  
  
    -   Zip  
  
## <a name="next-step"></a>下一步  
 [任务 2：手动添加域值](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
