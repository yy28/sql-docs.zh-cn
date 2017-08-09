---
title: "Microsoft SQL 和 GDPR 要求 | Microsoft Docs"
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql
ms.reviewer: 
ms.suite: 
ms.technology: sql-security
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 2
author: barbkess
ms.author: ronitr
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: d533818e9498237316dabc08fc538caa2ac31c63
ms.openlocfilehash: f236ff85204ba08e8c02d5e680a4de43f021b9aa
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="guide-to-enhancing-privacy-and-addressing-gdpr-requirements-with-the-microsoft-sql-platform"></a>增强隐私和使用 Microsoft SQL 平台应对 GDPR 要求的指南


## <a name="summary"></a>摘要
欧盟的一项隐私法律将于 2018 年 5 月 25 日生效，其中针对隐私权、安全性和合规性设定了新的全球禁令。 《一般数据保护条例》(GDPR) 主要用于保护个人隐私权和促进此权利的行使，其中设定了严格的全球隐私要求，旨在监管个人数据的管理和保护方式，同时尊重个人选择。 

Microsoft SQL 客户需遵守 GDPR，无论他们管理基于云的数据库还是本地数据库或两者兼有，都需要确保根据 GDPR 原则对其数据库系统中的合格数据进行合理处理和保护。 这意味着，许多客户将需要评审或修改其数据库管理和数据处理过程，尤其要重点关注 GDPR 中所规定的数据处理安全性。

基于 Microsoft SQL 的技术提供了许多内置安全功能，可帮助降低数据的风险，同时在数据库级别及更高级别改进对数据的保护和可管理性。 本指南将检验这些功能，并分享一些 Microsoft 自己的方法，使用 Microsoft SQL 实现 GDPR 的数据隐私目标。
   
  
**作者：**Ronit Reger

**技术审阅人员：**Conor Cunningham、Joachim Hammer、Shai Kariv、Julie Koesmarno、Alice Kupcik、Ron Matchoro、Gilad Mittelman、Dan Rediske、Tomer Weisberg 
  
**发布时间：**2017 年 5 月  
  
**适用于：**SQL Server（所有版本）、Azure SQL 数据库、Azure SQL 数据仓库、Analytics Platform System 
  
若要查看该文档，请下载[增强隐私和使用 Microsoft SQL 平台应对 GDPR 要求的指南](http://download.microsoft.com/download/4/9/4/4948194B-A613-49ED-90A5-5144313549AB/microsoft-sql-and-the-gdpr.pdf)文档。   

