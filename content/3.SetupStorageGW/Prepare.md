---
title: "׼������"
chapter: false
weight: 31
---

## ����Storage Gateway֮ǰ��׼������

���������ǻ����׼��������
1.����һ��IAM�û�
��¼ AWS �������̨����ͨ����ַhttps://console.amazonaws.cn/iam/home#/users$new?step=details�� ��IAM������̨������ʼ����һ���µ��û���
����һ���µ�IAM�û������������͡�ѡ��Programmatic access�����û���Ϊ��storagegateway-coldbackup����
![](/images/SetupStorageGW/addIAMUser.png)
��һ��ѡ��AWS����Ĳ��ԣ�AmazonS3FullAccess �� AWSStorageGatewayFullAccess
![](/images/SetupStorageGW/IAMPolicy1.png)
![](/images/SetupStorageGW/IAMPolicy2.png)
�����Ҫ��¼��Access Key��Secret Access Key�����Ʊ��档
![](/images/SetupStorageGW/AKSK.png)

2.����һ��S3 Bucket
��¼ AWS �������̨����ͨ����ַhttps://console.amazonaws.cn/s3/bucket/create?region=cn-northwest-1�� Amazon S3 ����̨������ʼ����һ���µ� S3�洢Ͱ 
Create bucket (�����洢Ͱ)���� Bucket name �ֶ��У�Ϊ�´洢Ͱ����һ������ DNS ��׼��Ψһ���ƣ��˴�����Ϊ��storagegateway-coldbackup-20200101xx�������� Region��ѡ����ΪҪ���洢Ͱ���õ�������ѡ��China (Ningxia) cn-northwest-1����Ȼ������Create bukcet����
![](/images/SetupStorageGW/createS3Bucekt.png)


