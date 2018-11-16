---
title: 在 JDBC FIPS 模式 |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: craigg
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: b99aa6be170402b0e8f18dddd578c1fb6c615dd6
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601867"
---
# <a name="fips-mode"></a>FIPS 模式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支持*FIPS 140 兼容模式下*。 适用于 Oracle / Sun JVM，请参阅[SunJSSE FIPS 140 兼容模式下](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html)启用部分提供的 Oracle 配置 FIPS 的 JVM。 

#### <a name="prerequisites"></a>必备条件

- FIPS 配置的 JVM
- 相应的 SSL 证书。
- 相应的策略文件。 
- 相应的配置参数。 


## <a name="fips-configured-jvm"></a>FIPS 配置的 JVM

若要查看的 FIPS 配置的已批准的模块，请参阅[验证 FIPS 140-1 和 FIPS 140-2 加密模块](https://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm)。 

供应商可能有一些附加步骤来配置与 FIPS 的 JVM。

### <a name="ensure-your-jvm-is-in-fips-mode"></a>确保 JVM 处于 FIPS 模式
若要确保已启用 FIPS JVM，请执行以下代码片段： 

```java
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
```

## <a name="appropriate-ssl-certificate"></a>相应的 SSL 证书
若要连接 SQL Server 在 FIPS 模式下，有效的 SSL 证书是必需的。 安装或导入 Java 密钥存储在客户端计算机 (JVM) 上启用了 FIPS。

### <a name="importing-ssl-certificate-in-java-keystore"></a>导入 Java 密钥存储中的 SSL 证书
Fips，很可能需要证书 (.cert) 导入到任一 PKCS 或特定于提供程序的格式。 使用以下代码片段导入 SSL 证书并将其存储在工作目录中具有相应的密钥存储格式。 _信任\_应用商店\_密码_Java 密钥存储的是你的密码。 


```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```


下面的示例导入带有 BouncyCastle 提供程序 PKCS12 格式的 Azure SSL 证书。 在名为的工作目录中导入证书_MyTrustStore\_PKCS12_通过使用以下代码片段：

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>相应的策略文件
对于 FIPS 某些提供程序，需要使用不受限制的策略 jar。 在这种情况下，sun / Oracle 下载 Java Cryptography Extension (JCE) 不受限制 Strength Jurisdiction Policy Files 有关[JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或[JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)。 

## <a name="appropriate-configuration-parameters"></a>相应的配置参数
若要在与 FIPS 兼容模式下运行 JDBC 驱动程序，请配置连接属性下, 表中所示。 

#### <a name="properties"></a>属性 

|“属性”|类型|，则“默认”|描述|说明|
|---|---|---|---|---|
|encrypt|布尔 [“true / false”]|“false”|启用 FIPS 的 JVM 加密属性应为 **，则返回 true**||
|TrustServerCertificate|布尔 [“true / false”]|“false”|Fips，用户需要验证证书链，因此，用户应使用 **"false"** 此属性的值。 ||
|trustStore|String|null|您可以导入你的证书为 Java 密钥存储文件路径。 如果您的系统，则无需传递任何内容安装证书。 驱动程序使用 cacerts 或 jssecacerts 文件。||
|trustStorePassword|String|null|用于检查 trustStore 数据完整性的密码。||
|fips|布尔 [“true / false”]|“false”|启用 FIPS 的 JVM 此属性应为 **，则返回 true**|添加在 6.1.4 (稳定版本 6.2.2)||
|fipsProvider|String|null|JVM 中配置的 FIPS 提供程序。 例如，BCFIPS 或 SunPKCS11 NSS |6.1.2 中添加 (稳定版本 6.2.2)，已弃用在 6.4.0-请参阅详细信息[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)。|
|trustStoreType|String|JKS|FIPS 模式下将信任存储区类型设置为 PKCS12 或类型由 FIPS 提供程序定义 |6.1.2 中添加 (稳定版本 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

