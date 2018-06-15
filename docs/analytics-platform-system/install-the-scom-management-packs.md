---
title: 安装 SCOM 管理包-分析平台系统 |Microsoft 文档
description: 请按照下列步骤以下载并安装 System Center Operations Manager (SCOM) 管理包适用于 SQL Server PDW。 监视 SCOM 中的 SQL Server PDW 所需管理包。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 163ab893074e171decb573d876c5f98334437985
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544679"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>针对分析平台系统中安装 SQL Server Operations Manager (SCOM) 管理包
请按照下列步骤以下载并安装 System Center Operations Manager (SCOM) 管理包适用于 SQL Server PDW。 监视 SCOM 中的 SQL Server PDW 所需管理包。  
  
## <a name="BeforeBegin"></a>开始之前  
**先决条件**  
  
System Center Operations Manager 必须已安装并且正在运行。 SQL Server PDW 2012 需要 System Center Operations Manager 2007 R2、 System Center Operations Manager 2012 或 System Center Operations Manager 2012 service pack 1。  
  
## <a name="Step1"></a>步骤 1： 下载管理包  
对于 APS PDW 工作负荷，下载[System Center Management Pack for Microsoft Analytics Platform System](http://go.microsoft.com/fwlink/?LinkId=396857)。  
  
有关设备管理，下载[SQL Server 设备基本管理包](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11436)。  
  
对于较旧版本的 PDW 不 AP 的情况下，下载[针对 Microsoft SQL Server 2012 并行数据仓库设备的 System Center 监视包](http://go.microsoft.com/fwlink/p/?LinkId=282661)。  
  
HDInsight 上的工作负载，下载[适用于 HDInsight 的 System Center 管理包](http://go.microsoft.com/fwlink/?LinkId=390208)。  
  
## <a name="Step2"></a>步骤 2： 安装的管理包  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>安装 SQL Server 设备的基本管理包  
  
1.  若要运行安装，请双击下载的 SQL Server 设备基本管理包。  
  
2.  接受许可协议，然后单击**下一步**。  
  
    ![接受许可协议](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  选择你自己的安装文件夹，或使用默认管理包安装文件夹。  
  
    ![选择安装文件夹](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  单击 **“安装”**。  
  
    ![确认安装](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  单击 **“关闭”**。  
  
    ![单击关闭](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>安装适用于 SQL Server PDW 设备的监视包  
  
1.  若要运行安装，请双击下载的 SQL Server PDW 设备管理包。  
  
2.  接受许可协议，然后单击**下一步**。  
  
    ![接受许可协议](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  选择将保存提取的文件的目录。 默认情况下显示的默认管理包安装文件夹。 选择默认值，或选择你自己的安装文件夹。  
  
    ![选择安装文件夹](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  单击 **“安装”**。  
  
    ![确认安装](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  单击 **“关闭”**。  
  
    ![安装完成](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>下一步  
现在，你已安装的管理包，继续执行下一步： [SCOM 管理包导入用于 PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
