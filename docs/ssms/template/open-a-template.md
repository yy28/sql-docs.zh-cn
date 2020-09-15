---
description: 打开模板
title: 打开模板
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 730963488d34750ead61fe2662eb8201f91b30e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417853"
---
# <a name="open-a-template"></a>打开模板
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
可以从模板资源管理器中打开模板。  
  
## <a name="to-open-a-template-from-template-explorer"></a>从模板资源管理器中打开模板  
可以从模板资源管理器中打开模板。  
  
1.  若要打开模板资源管理器，请在“视图”**** 菜单上单击“模板资源管理器”****。  
  
2.  在模板类别列表中，展开包含要打开的模板的类别。  
  
3.  有三种方法可以打开模板：  
  
    1.  双击模板以在代码编辑器窗口中将其打开。  
  
    2.  右键单击模板并选择“打开”**** 以在代码编辑器窗口中将其打开。  
  
    3.  将模板拖到代码编辑器窗口，以将模板代码添加到编辑器窗口的内容中。  
  
打开模板之后，使用“替换模板参数”**** 对话框将模板参数替换为具体的值。  
  
如果打开模板启动了一个新的编辑器窗口，将使用当前活动连接的凭据打开该窗口。 例如，如果在打开 CREATE DATABASE 模板时聚焦对象资源管理器中的某个 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 实例，将使用到该实例的连接打开新的编辑器窗口。 如果没有活动连接， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 将显示登录对话框。  
  
## <a name="see-also"></a>另请参阅  
[模板资源管理器](../../ssms/template/template-explorer.md)  
[替换模板参数](../../ssms/template/replace-template-parameters.md)  
  
