---
title: 设置历史记录保持期 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 13dcf2ad9a9d619a7fdef9c1ed3f7b970e420cdd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055645"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>设置历史记录保持期 (SQL Server Management Studio)
  在 "**分发数据库属性 \<DistributionDatabase> -** " 对话框的 "**常规**" 页上指定历史记录保持期。 此设置控制复制代理历史记录可存储的时间。 可以从 "**分发服务器属性 \<Distributor> -** 对话框的"**常规**"页中访问此页。 有关访问此对话框的详细信息，请参阅[查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-history-retention-period"></a>指定历史记录保持期  
  
1.  在 "**分发服务器属性- \<Distributor> ** " 对话框的 "**常规**" 页上，单击分发数据库的属性按钮（**...**）。  
  
2.  在 **“至少存储复制性能的历史记录”** 框中输入一个值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [配置分发](configure-distribution.md)  
  
  
