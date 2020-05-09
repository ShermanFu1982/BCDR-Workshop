---
title: "�������ݵ�Stroage Gateway��"
chapter: false
weight: 32
---

## ������������ʹ��AWS Storage Gateway��ΪNAS�洢�������ļ�����

�����������˽�һ�±�������������ʹ���ļ��洢���صĵ������̡��û���Ӧ�÷����������ڱ������������ڣ����û������в����ļ��洢���أ�File Gateway����
Ȼ���û���Ӧ�÷�����ͨ��NFS�ͻ������Ӵ洢���أ��������ؽ� S3 �еĴ洢Ͱ��Ϊ NFS �ƶ˴洢���Ӷ����ļ�����д��ͷ��ʡ�
�������ڱ��ؽ� File Gateway ��Ϊ����� (VM) �豸���У�Ŀǰ֧�ֵ����⻯������VMware ESXi��Microsoft Hyper-V��Linux �ں˵������ (KVM)��
��������ɲο���https://docs.aws.amazon.com/zh_cn/storagegateway/latest/userguide/Requirements.html �� http://docs.aws.amazon.com/zh_cn/storagegateway/latest/userguide/deploy-gateway-vmware.html

����ʵ�����AWS EC2 ʵ�� �C ��������File Gateway �ļ��洢���أ���ԭ����������� (VM) �豸��������ͬ��ֻ�Ǵ���ϸ�����в�ͬ����������������£�
1.����Storage Gateway
��https://console.amazonaws.cn/storagegateway/create/gateway?region=cn-north-1����Storage Gateway, ѡ�� File Gateway���ļ��洢�������͡�
��Ҫע����ǣ�����ʵ�齫��cn-north-1 Beijing ���򴴽��ļ��洢���أ���Ϊ���ǵı����������Ĳ����ڱ���region��
![](/images/SetupStorageGW/createStorageGW.png)

2.ѡ��Amazon EC2��Ϊ����ƽ̨����������˵������VPC���������ͣ������EBS����ȫ��ȡ�
ע�⣺
* ��Ҫ��EC2����Ҫ����ڻ����xlarge����4��/16G�ڴ档����ʹ��m5.xlarge��
![](/images/SetupStorageGW/createStorageGW-EC2.png)
![](/images/SetupStorageGW/createStorageGW-EC2Type.png)
* ��Ҫ�������EBS�����������ò�ӦС��150G�����洢����������Ҫ���һ�������Ա���л��棬�ͻ��˶��ļ��ķ��ʻ������ڻ�����ȥ��ȡ�ļ���Ϣ��������������ͨ������ȥS3ֱ�ӻ�ȡ�ļ����ӳ٣��ļ��洢���ػ������ֵΪ16TB��
![](/images/SetupStorageGW/createStorageGW-EBS.png)
* �ڰ�ȫ������ʱ���ð�ȫ���ԣ�����VPC����������ͨ��80�˿ڷ��ʸû�������ʱ����http 80�˿ڣ�
![](/images/SetupStorageGW/createStorageGW-SG.png)
* ��֤��EC2ʵ���ܹ����ʹ���

3.���Gateway˽��IP
�ȴ�EC2������ɣ����https://console.amazonaws.cn/ec2/v2/home?region=cn-north-1����EC2����ҳ����¼�¸û�����˽��IP �����ĳ�Ϊ Gateway˽��IP��
![](/images/SetupStorageGW/createStorageGW-IP.png)

4.���Ӳ���������
SSH��¼�������EC2ʵ����������������õ�File Gatewayʵ���ļ����룺
```bash
curl -I [gateway˽��IP]/?activationRegion=cn-north-1
```
��¼�¼�����activationKey��ֵ
![](/images/SetupStorageGW/activateStorageGW.png)

5.�������������File Gateway
```bash
aws --region cn-north-1 storagegateway activate-gateway --activation-key [activationKey] --gateway-type FILE_S3 --gateway-name [gateway name] --gateway-timezone GMT+8:00 --gateway-region cn-north-1
```
����ɹ��������GatewayARN
![](/images/SetupStorageGW/gatewayARN.png)

6.����File Gateway����
��https://console.amazonaws.cn/storagegateway/home/gateways?region=cn-north-1�����File Gateway�Ƿ��Ѿ�������Offine״̬����Ҫ��һ�ᣩ��
���File Gateway���༭���ش��̣�������ʱ��ӵ�EBS�����óɻ��棬���ұ��档
![](/images/SetupStorageGW/gatewayCache1.png)
![](/images/SetupStorageGW/gatewayCache2.png)

7.�����ļ���������S3 bucket����File Gateway
��https://console.amazonaws.cn/storagegateway/create/file-share?region=cn-north-1 �󴴽��ļ����� S3 bucketΪ׼���׶δ�����S3�洢Ͱ ��storagegateway-coldbackup-20200101xx��������ѡ�� sg02_onprem-bjs-az1-dmz��������Э��ΪNFS��
![](/images/SetupStorageGW/S3AndGateway1.png)
![](/images/SetupStorageGW/S3AndGateway2.png)

8.��EC2��ʹ��file gateway�ϵ�NFS
��¼�Ѿ���������ʱEC2ʵ�������ǽ��ڸû����ϲ���NFS�����ã������������
```bash
sudo mount -t nfs -o nolock [gateway˽��IP]:/[s3�洢Ͱ��] [MountPath]
```
![](/images/SetupStorageGW/mountFS.png)

9.�ɹ�mount�����Ϳ�����/nfs�ļ��п���s3�洢Ͱ�е������ˡ����������,ɾ��,���߲鿴��Щ���ݡ�
```bash
cd [MountPath]
echo "hello, one" > hello1.txt 
echo "hello, two" > hello2.txt
echo "hello, three" > hello3.txt
```
![](/images/SetupStorageGW/backupFileToGW.png)

��¼ AWS �������̨����ͨ����ַhttps://console.amazonaws.cn/s3/home?region=cn-north-1�� Amazon S3 ����̨������� storagegateway-coldbackup-20200101xx���洢Ͱ��
![](/images/SetupStorageGW/verifyBackup.png)

{{% notice note %}}
ע�⣺ ����/nfs�ļ����µ��κβ�����ֱ��ӳ�䵽File Gateway�����ϣ�Ϊ������Ч�ʣ�����ᶨ�ں�S3����ͬ�����������ԣ����������һ���ļ���/nfs�У�������Ҫ��������S3�洢Ͱ�п�������
{{% /notice  %}}
