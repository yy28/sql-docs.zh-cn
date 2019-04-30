---
title: 安装 SCOM 管理包的分析平台系统 |Microsoft Docs
description: 请按照下列步骤以下载并安装用于 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理包。 监视 SCOM 中的 SQL Server PDW 所需的管理包。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f0acfa636a3432dcffb18cfec57ee7625c1eb01b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215536"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>针对分析平台系统中安装 SQL Server Operations Manager (SCOM) 管理包
请按照下列步骤以下载并安装用于 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理包。 监视 SCOM 中的 SQL Server PDW 所需的管理包。  
  
## <a name="BeforeBegin"></a>开始之前  
**先决条件**  
  
System Center Operations Manager 必须已安装并正在运行。 SQL Server PDW 2012 需要 System Center Operations Manager 2007 R2 中，System Center Operations Manager 2012 或 System Center Operations Manager 2012 service pack 1。  
  
## <a name="Step1"></a>步骤 1:下载管理包  
对于 APS PDW 工作负荷，下载[System Center 管理包 Microsoft Analytics Platform system](https://go.microsoft.com/fwlink/?LinkId=396857)。  
  
对于设备管理中下载[SQL Server 设备基本管理包](https://www.microsoft.com/download/details.aspx?displaylang=en&id=11436)。  
  
对于较旧版本的 PDW 而无需 AP，下载[System Center Monitoring Pack for Microsoft SQL Server 2012 并行数据仓库工具](https://go.microsoft.com/fwlink/p/?LinkId=282661)。  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>步骤 2:安装管理包  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>安装 SQL Server 设备基础管理包  
  
1.  若要运行安装，请双击下载的 SQL Server 设备基本管理包。  
  
2.  接受许可协议，然后单击**下一步**。  
  
    ![接受许可协议](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  选择你自己的安装文件夹，或使用默认管理包安装文件夹。  
  
    ![选择安装文件夹](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  单击 **“安装”**。  
  
    ![确认已安装](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  单击 **“关闭”**。  
  
    ![单击关闭](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>安装适用于 SQL Server PDW 设备的监视包  
  
1.  若要运行安装，请双击下载的 SQL Server PDW 设备管理包。  
  
2.  接受许可协议，然后单击**下一步**。  
  
    ![接受许可协议](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  选择将保存提取的文件的目录。 默认情况下显示的默认管理包安装文件夹。 选择默认值，或选择安装文件夹。  
  
    ![选择安装文件夹](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  单击 **“安装”**。  
  
    ![确认已安装](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  单击 **“关闭”**。  
  
    ![安装完成](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>下一步  
现在，已安装的管理包，继续下一步：[SCOM 管理包为 PDW 导入&#40;分析平台系统&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
