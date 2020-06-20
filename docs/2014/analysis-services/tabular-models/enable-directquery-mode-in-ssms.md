---
title: 为表格模型数据库配置内存中或 DirectQuery 访问权限 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 145d5a0d32384a0bcea1d60d00dcf3988642229c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938908"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>为表格模型数据库配置内存中或 DirectQuery 访问
  本主题介绍如何更改已部署的表格模型的连接属性，以便能在直接查询模式下使用模型。  
  
 有关这些属性以及最常见方案的配置的详细信息，请参阅[DirectQuery 部署方案 &#40;SSAS 表格&#41;](../directquery-deployment-scenarios-ssas-tabular.md)。  
  
## <a name="requirements"></a>要求  
 允许在表格模型中使用直接查询模式是一个多步骤过程。 必须具备以下条件：  
  
1.  确保该模型具有的功能不会导致直接查询模式中出现验证错误。  
  
2.  更改模型中的存储模式以支持直接查询。  
  
3.  在支持混合或纯直接查询模式中的查询的模式下部署该模型。  
  
4.  在已部署的数据库上编辑连接字符串以支持直接查询模式。  
  
 本主题假定您已创建并验证您的模型，且只需从客户端（如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]）启用直接查询访问。  
  
## <a name="procedure"></a>过程  
  
#### <a name="change-the-connection-string-properties-of-the-model"></a>更改模型的连接字符串属性  
  
1.  在 SQL Server Management Studio 中，打开已将模型部署到的实例。  
  
2.  在对象资源管理器中，右键单击 model 数据库的名称，然后选择 "**属性**"。  
  
3.  找到 " **DirectQueryMode**" 属性。 若要允许使用关系数据源，则必须将此属性设置为下列值之一：  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  
