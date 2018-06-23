---
title: 安装 ADO.NET Data Services 以支持数据源的 SharePoint 列表导出 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: d4241d56aa3257bd0ec2cddf4b439a4939f8ab9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018512"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>安装 ADO.NET Data Services 以支持 SharePoint 列表的数据馈送导出
  ADO.NET Data Services 是 SharePoint 列表的数据馈送导出所必需的。 SharePoint 2010 在 SharePoint Prerequisite Installer 程序中不包括此组件，因此您必须手动安装它。  
  
 如果没有此先决条件，当您使用导出为数据馈送的 SharePoint 列表时，您将获得以下错误：“DTD 出于安全原因已在此 XML 文档中禁用。 若要启用 DTD 处理，请将 XmlReaderSettings 的 ProhibitDtd 属性设置为 false，并将设置传递到 XmlReader.Create 方法。“  
  
 使用以下说明在您想要允许列表作为数据馈送导出的每个 SharePoint 服务器上安装 ADO.NET Data Services。  
  
### <a name="download-and-install-adonet-data-services"></a>下载和安装 ADO.NET Data Services  
  
1.  转到 SharePoint 2010 的硬件和软件要求文档[硬件和软件要求 (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  在**适用的软件访问**，找出有关 ADO.NET Data Services 3.5 对应于操作系统 （Windows Server 2008 SP2 或 Windows Server 2008 R2） 使用的链接。  
  
3.  单击该链接并且运行安装该服务的安装程序。  
  
## <a name="see-also"></a>请参阅  
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  