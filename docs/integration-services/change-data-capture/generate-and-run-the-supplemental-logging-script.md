---
title: "生成和运行补充日志记录脚本 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee20cd83df04d4ec3929f9ee39068969c0d18950
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>生成和运行补充日志记录脚本
  使用“为捕获变更设置表”页可对 Oracle 源数据库运行一个将设置补充日志记录的脚本。  
  
 **运行补充日志记录脚本**  
  
 单击 **“运行脚本”** 可对为 CDC 实例定义的表运行补充日志记录脚本。 此脚本指示 Oracle 数据库在将 UPDATE 操作记录到捕获表时将有关的所有列写入其事务日志。 此脚本通常由 Oracle 系统管理员检查和执行。  
  
 您还可以使用 SQL * Plus 手动运行脚本。  
  
 **手动运行脚本**  
  
 单击 **“复制”** 将脚本粘贴到剪贴板。 打开 SQL* Plus 并且转到具有您的 Oracle 源数据库的目录。 将脚本粘贴到 SQL\*Plus 中，以便运行该脚本。  
  
 若要在文本文件中保存补充日志记录脚本，请单击 **“另存为”** 并且浏览到要保存该文件的位置。 为该文件提供一个名称，然后单击 **“保存”** 以便保存该文件。  
  
 单击 **“下一步”** 以便 [Generate Mirror Tables and CDC Capture Instances](../../integration-services/change-data-capture/generate-mirror-tables-and-cdc-capture-instances.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何创建 SQL Server 更改数据库实例](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [查看和生成补充日志记录脚本](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
