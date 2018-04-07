---
title: 安装 SCOM 管理包 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab3985d8-0a71-4b28-9d28-9886ae2a110f
caps.latest.revision: 16
ms.openlocfilehash: 2f05a947f09940fc1dd676ec6ca316863f567a7f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="install-the-scom-management-packs"></a>安装 SCOM 管理包
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
  
