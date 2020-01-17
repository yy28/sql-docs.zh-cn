---
title: 将基于策略的管理 Facet 状态复制到 XML 文件
description: 介绍如何使用 SQL Server Management Studio (SSMS) 将基于策略的管理 Facet 状态复制到 XML 文件。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fa0ee70601b11af3341483aff177ef6a7a389ba6
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558183"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>将基于策略的管理方面状态复制到 XML 文件中
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中将基于策略的管理方面的状态复制到 XML 文件中。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要将方面状态复制到 XML 文件中，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 本主题中的过程要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>将方面状态复制到 XML 文件中  
  
1.  在对象资源管理器中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例、实例对象、数据库或数据库对象，然后单击“Facet”  。  
  
2.  在“查看 Facet - object_name”对话框中，单击“将当前状态导出为策略”    。  
  
3.  在“导出为策略”  对话框中，键入该文件的路径和名称；或者使用“浏览”按钮 **(...)** 查找该文件，然后键入该 XML 文件的名称。 有关此对话框中可用选项的详细信息，请参阅 [Export As Policy Dialog Box](../../relational-databases/policy-based-management/export-as-policy-dialog-box.md)。  
  
4.  完成后，单击 **“确定”** 。  
  
  
