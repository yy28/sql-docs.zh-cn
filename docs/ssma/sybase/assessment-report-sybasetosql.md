---
title: 评估报表 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aae49bb6eb8ecf067911b2cb64017af0f3143aa0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132799"
---
# <a name="assessment-report-sybasetosql"></a>评估报表 (SybaseToSQL)
评估报告窗口会显示到的数据库对象的转换的结果[!INCLUDE[tsql](../../includes/tsql-md.md)]语法，并且还可以帮助您评估的复杂性和成本在迁移项目。  
  
若要访问评估报表中，选择对象要转换源元数据资源管理器中右键单击**数据库**，然后选择**创建报表**。  
  
## <a name="options"></a>选项  
**转换的统计信息**  
显示按语句类型的转换统计信息。 此窗格是一个组对象，如架构时才可见，或在左窗格中选择而无需代码的对象。  
  
**按类别列出的对象**  
显示按对象类型的转换统计信息。 此窗格是一个组对象，如架构时才可见，或在左窗格中选择而无需代码的对象。  
  
**统计信息**  
显示所选对象的转换统计信息。 仅当在左窗格中选择具有代码的单个对象时，会显示此窗格。 您可能需要展开**统计信息**若要查看此窗格。  
  
**源导航功能**  
显示所选对象的 ASE 代码并突出显示不转换为代码[!INCLUDE[tsql](../../includes/tsql-md.md)]。 仅当在左窗格中选择具有代码的单个对象时，会显示此窗格。  
  
单击要设置或清除书签的行号。 使用在窗格的顶部按钮代码中导航。  
  
**目标导航**  
显示了转换的生成[!INCLUDE[tsql](../../includes/tsql-md.md)]所选的对象和未转换的代码的错误消息代码。 仅当在左窗格中选择具有代码的单个对象时，会显示此窗格。  
  
单击要设置或清除书签的行号。 使用在窗格的顶部按钮代码中导航。  
  
**消息窗格**  
显示错误、 警告和信息性消息时创建评估报告生成。 消息按数字进行分组。 若要查看导致了错误的代码，请单击**错误**，**警告**，或**信息**，展开的消息，类别，然后单击一条消息。  
  
