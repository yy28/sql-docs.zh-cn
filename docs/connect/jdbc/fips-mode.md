---
title: FIPS 模式下 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.workload: Inactive
ms.openlocfilehash: bc357dc09c8357db8c9a5de24d6644029f31dd14
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="fips-mode"></a>FIPS 模式下
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支持*FIPS 140 兼容模式下*。 适用于 Oracle / Sun JVM，请参阅[SunJSSE FIPS 140 兼容模式下](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html)部分提供的 Oracle 配置 FIPS 启用 JVM。 

**先决条件**:
* FIPS 配置 JVM
* 相应的 SSL 证书。
* 相应的策略文件。 
* 相应的配置参数。 


## <a name="fips-configured-jvm"></a>FIPS 配置 JVM

若要查看针对 FIPS 配置的已批准的模块，请参阅[验证 FIPS 140-1 和 FIPS 140-2 加密模块](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm)。 

供应商可能有一些附加步骤以使用 FIPS 配置 JVM。

### <a name="ensure-your-jvm-is-in-fips-mode"></a>确保你 JVM 处于 FIPS 模式下
为了确保你 JVM 是启用的 FIPS，执行下面的代码段： 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>相应的 SSL 证书
若要在 FIPS 模式下连接 SQL Server，有效的 SSL 证书是必需的。 安装或将其导入 Java 密钥上的存储客户端计算机 (JVM) 启用 FIPS。 如果您不未导入 / 安装适当的证书，你可能无法连接到 SQL Server，因为无法建立安全连接。

### <a name="importing-ssl-certificate-in-java-keystore"></a>导入 Java 密钥库中的 SSL 证书
对于 FIPS，很可能你需要证书 (.cert) 导入到任一 PKCS 或提供程序特定格式。 使用下面的代码段导入 SSL 证书并将其存储在工作目录中具有相应的密钥库格式。 _TRUST_STORE_PASSWORD_为 Java 密钥库是您的密码。 

````
    public void saveGenericKeyStore(String provider, String trustStoreType, String certName, String certPath) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, NoSuchProviderException, IOException {
        KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
        FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
        ks.load(null, null);
        ks.setCertificateEntry(certName, getCertificate(certPath));
        ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
        os.flush();
        os.close();
    }

    private Certificate getCertificate(String pathName) throws FileNotFoundException, CertificateException {
        FileInputStream fis = new FileInputStream(pathName);
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        return cf.generateCertificate(fis);
    }

````


下面的示例导入带有 BouncyCastle 提供程序 PKCS12 格式的 Azure SSL 证书。 命名的工作目录中导入证书_MyTrustStore_PKCS12_通过使用下面的代码段：

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>相应的策略文件
对于 FIPS 某些访问接口，需要使用不受限制的策略 jar。 在这种情况下，对于 Sun / Oracle，下载的 Java 加密扩展 (JCE) 不限强度管辖策略文件[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或[JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)。 

## <a name="appropriate-configuration-parameters"></a>相应的配置参数
若要在符合 fips 标准的模式下运行 JDBC 驱动程序，配置相应的连接属性下, 表中所示。 

**属性**: 

|属性|类型|默认|Description|说明|
|---|---|---|---|---|
|encrypt|布尔值 ["true / false"]|"false"|JVM FIPS 已启用加密属性应为**true**||
|TrustServerCertificate|布尔值 ["true / false"]|"false"|针对 FIPS，用户需要验证证书链，以便用户应使用 **"false"** 此属性的值。 ||
|trustStore|字符串|null|你可以导入你的证书你 Java 密钥库文件路径。 如果你的系统，则无需传递任何内容安装证书。 驱动程序使用 cacerts 或 jssecacerts 文件。||
|trustStorePassword|字符串|null|用于检查 trustStore 数据完整性的密码。||
|fips|布尔值 ["true / false"]|"false"|此属性对于 fips 启用 JVM 应为**true**|添加在 6.1.4 (稳定版本 6.2.2)||
|fipsProvider|字符串|null|在 JVM 中配置的 FIPS 提供程序。 例如，BCFIPS 或 SunPKCS11 NSS |添加在 6.1.2 (稳定释放 6.2.2)，在 6.4.0-中已过时，请参阅详细[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)。|
|trustStoreType|字符串|JKS|对于 FIPS 模式集信任存储区类型 PKCS12 或类型由定义 FIPS 提供程序 |添加在 6.1.2 (稳定版本 6.2.2)||



  
