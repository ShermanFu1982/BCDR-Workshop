---
title: "��Stroage Gateway�ϻָ�����"
chapter: false
weight: 33
---

## ��AWS Storage Gateway�����ļ��ָ�

ʹ��AWS Storage Gateway��ΪNAS�洢���ָ��ļ��Ĺ����뱸�����ƣ�������Ҫ�ȴ����ļ����ز����Ȼ�󴴽��ļ��������ļ���������ɱ��ݵ�S3 bucket���й�����

{{% notice note %}}
Ψһ��ͬ���ǣ���Ҫ���ļ�������ʾ���á�ˢ�»��桱�����������Ļ�ȡAmazon S3 �洢Ͱ�еĶ���
{{% /notice  %}}

* ��Ϊ�� NFS�ͻ���ִ���ļ�ϵͳ����ʱ���������ػ������ļ���������� Amazon S3 �洢Ͱ��ά��һ�������嵥������ʹ�ô˻����嵥����С S3 ������ӳٺ�Ƶ�ʡ�
* һ���µ��ļ����ع�����Amazon S3 �洢Ͱ����Ҫͨ����ʾˢ������ɶ����嵥�ĸ��£��Ӷ�����NFS�ͻ��˲�ѯ���������ļ��嵥��
* ˢ�¹��������ʱ��ȡ�����������ϻ���Ķ������Լ��� S3 �洢Ͱ����ӻ�ɾ���Ķ�������

Ҫˢ�������ļ������ S3 �洢Ͱ��������ʹ�� AWS Storage Gateway ����̨�� AWS Storage Gateway API �е� RefreshCache ��������������������£�
1.�����µ��ļ����أ�����S3 bucket�洢Ͱ�󣬷��� NFS�ͻ��� �޷���ѯ��S3 bucket�洢Ͱ���е��ļ�������ͼ��
![](/images/SetupStorageGW/restoreFromStorageGW1.png)
![](/images/SetupStorageGW/restoreFromStorageGW2.png)

2.ˢ���ļ����شӶ������Ļ�ȡAmazon S3 �洢Ͱ�еĶ��������������
```bash
aws storagegateway list-file-shares #���file share ARN
aws storagegateway refresh-cache -�Cfile-share-arn <fileshare ARN> #����RefreshCache
```
ͨ����������RefreshCache��� NFS�ͻ��˳ɹ���ѯ��S3 bucket�洢Ͱ���е��ļ���
![](/images/SetupStorageGW/listFileShare.png)

