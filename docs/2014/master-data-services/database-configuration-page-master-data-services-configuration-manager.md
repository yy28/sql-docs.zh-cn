---
title: 数据库配置页（Master Data Services 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.dbpg.f1
ms.assetid: dd72220e-a599-465d-8b84-9bb6a7433216
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7f5f11ba4154b70c5aa1fd0ae0e7579c746ce744
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483187"
---
# <a name="database-configuration-page-master-data-services-configuration-manager"></a>“数据库配置”页（Master Data Services 配置管理器）
  使用 **“数据库配置”** 页可以编辑 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的系统设置。 系统设置将影响与所选 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库相关联的所有 Web 应用程序和 Web 服务。 您必须首先选择或创建一个 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库，然后系统设置才能启用并且可用于配置。  
  
## <a name="current-database"></a>当前数据库  
 选择一个现有 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库或创建要编辑其系统设置的新数据库。 在创建后，将选择这个新数据库。  
  
|控件名称|Description|  
|------------------|-----------------|  
|**SQL Server 实例**|显示所选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称。 在您连接到某一实例并选择或创建某一 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库之前，此项为空。|  
|**Master Data Services 数据库**|显示所选 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的名称。 在您连接到某一实例并选择或创建某一 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库之前，此项为空。|  
|**Master Data Services 数据库版本**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库架构的版本。|  
|**创建数据库**|打开 **“创建数据库”** 向导，从中您可以连接到某一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例并为该实例创建 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。|  
|**选择数据库**|打开 **“连接到数据库”** 对话框，在其中连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例并选择 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。|  
|**升级数据库**|打开向导，您可以在其中升级指定的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。 仅当指定的数据库需要升级时，此按钮才会启用。|  
|**修复数据库**|单击此按钮以确保 MDS 数据库安装正确。 这在将 MDS 数据库备份并还原到从未托管过 MDS 数据库的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的情况下非常有用。|  
  
## <a name="system-settings"></a>系统设置  
 为与所选 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库相关联的所有 Web 应用程序和 Web 服务编辑系统设置。  
  
 这些设置在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中提供，并存储在数据库的系统设置表 (mdm.tblSystemSetting) 中。 有关所有设置的列表，请参阅[系统设置 (Master Data Services)](system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [为 Master Data Services 数据库和网站设置](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [数据库要求 (Master Data Services)](install-windows/database-requirements-master-data-services.md)  
  
  
