---
title: "[cloud]紀錄雲端儲存服務MinIO與Amazon S3開發筆記"
tags:
  - cloud
  - storage
  - aws-s3
  - MinIO
categories:
  - Tech.
  - cloud
  - storage
date: 2021-04-28 19:26:23
---


{% note info %} 簡單紀錄雲端儲存服務MinIO與Amazon S3與使用GO SDK開發筆記" {% endnote %}


<!--more-->


## Amazon Web Services (AWS) S3

*Amazon Web Services (AWS) S3，全名為亞馬遜簡易儲存服務，是亞馬遜公司利用其亞馬遜網路服務系統所提供的網路線上儲存服務。(目前可申請免費12個月)，沒有限制，就是用多少付多少錢，可以設定 Billing alert．


如果你有申請AWS帳號，可以用AWS SDK操作上傳到AWS S3，
s3沒有免費開發模擬器，只能註冊使用，但有其他可替代的兼容服務。
剛開始開發時因為沒有申請帳號，所以使用minIO替代．


## minIO
> MinIO是與Amazon S3兼容的服務器端存儲協議，可以處理最大對像大小為5TB的非結構化數據，例如照片，視頻，日誌文件，備份和容器映像，並附帶web ui介面。
官方文檔:https://docs.min.io/cn/
### minIO server
#### 1.自行建立安裝minIO server
各種安裝方式:https://docs.min.io/cn/minio-quickstart-guide.html


- Windows系统 執行檔安裝
https://dl.min.io/server/minio/release/windows-amd64/minio.exe
```
執行minio.exe server D:\Photos
預設開啟9000
RootUser: minioadmin
RootPass: minioadmin
```

- Windows docker
```
docker run -p 9000:9000 --name minio1 -v D:\data:/data -e "MINIO_ROOT_USER=AKIAIOSFODNN7EXAMPLE" -e "MINIO_ROOT_PASSWORD=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" minio/minio server /data
```

1.接著開啟:http://127.0.0.1:9000/，輸入上面的資訊就可以登入，
2.新增一個bucket，
3.然後上傳檔案成功，
4.上傳的檔案就會出現在 D:\data裡。

但簡單建立的版本並沒有Https，設定上教學裡的win載點已不在..，有興趣可以看這篇安裝:[使用TLS安全的访问Minio服务](https://docs.min.io/cn/how-to-secure-access-to-minio-server-with-tls.html)

*HTTPS經由HTTP進行通訊，但利用SSL/TLS來加密封包

-------------------------------
#### 2.使用官方提供建立好的minIO server  

```
https://play.min.io
 Play uses access_key_id Q3AM3UQ867SPQQA43P2F, secret_access_key zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG.
GUI操作:https://play.min.io/
```

### minIO client
#### mc
MinIO Client (mc)为ls，cat，cp，mirror，diff，find等UNIX命令提供了一种替代方案。它支持文件系统和兼容Amazon S3的云存储服务（AWS Signature v2和v4）。

有興趣可以至[MinIO客户端快速入门指南](https://docs.min.io/cn/minio-client-quickstart-guide.html)

#### minIO SDK
自行寫程式撰寫，範例:[Golang-minIO](https://docs.min.io/cn/golang-client-quickstart-guide.html)
- 首先使用minio-go
```
go get -u github.com/minio/minio-go
```

- 加入範例
自行替換以下endpoint/accessKeyID/secretAccessKey/useSSL資訊
```go 這個範例是使用minIO的SDK的範例  https://docs.min.io/cn/golang-client-quickstart-guide.html golang-client-quickstart-guide
package main

import (
	"context"
	"log"
	minio "github.com/minio/minio-go/v7"
	"github.com/minio/minio-go/v7/pkg/credentials"
)
//1.先要建立minIO server
func main() {
	// endpoint := "play.min.io"
	// accessKeyID := "Q3AM3UQ867SPQQA43P2F"
	// secretAccessKey := "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG"
	//useSSL := true
	endpoint := "127.0.0.1:9000"
	accessKeyID := "AKIAIOSFODNN7EXAMPLE"
	secretAccessKey := "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
	useSSL := false //error http: server gave HTTP response to HTTPS client

	// 初使化 minio client对象。
	minioClient, err := minio.New(endpoint, &minio.Options{
		Creds:  credentials.NewStaticV4(accessKeyID, secretAccessKey, ""),
		Secure: useSSL,
	})
	if err != nil {
		log.Printf("err\n")
		log.Fatalln(err)
	}

	log.Printf("ok\n") // minioClient初使化成功

	// 创建一个叫mymusic的存储桶。
	bucketName := "test11"
	location := "us-east-1"
	ctx := context.Background()
	err = minioClient.MakeBucket(ctx, bucketName, minio.MakeBucketOptions{Region: location})
	if err != nil {
		// 检查存储桶是否已经存在。
		exists, errBucketExists := minioClient.BucketExists(ctx, bucketName)
		if errBucketExists == nil && exists {
			log.Printf("We already own %s\n", bucketName)
		} else {
			log.Printf("err\n")
			log.Fatalln(err)
		}
	} else {
		log.Printf("Successfully created %s\n", bucketName)
	}

	// 上传一个zip文件。
	objectName := "ssss.zip"
	filePath := "./ssss.zip"
	contentType := "application/zip"

	// 使用FPutObject上传一个zip文件。
	n, err := minioClient.FPutObject(ctx, bucketName, objectName, filePath, minio.PutObjectOptions{ContentType: contentType})
	if err != nil {
		log.Fatalln(err)
	}

	log.Printf("Successfully uploaded %s of size %d\n", objectName, n)

}

```



####  AWS SDK
如果你有用AWS S3的SDK，一樣可以使用它撰寫程式連結到minIO的server，
MinIO官方範例:[How to use AWS SDK for Go with MinIO Server](https://docs.min.io/docs/how-to-use-aws-sdk-for-go-with-minio-server.html)，不過該AWS ADK已經有V2了，如果用V2版需要再改一下自行定義資訊的寫法[Overriding Endpoint with Fallback](https://aws.github.io/aws-sdk-go-v2/docs/configuring-sdk/endpoints/)，或是讀取AWS config的本地Credentials資訊。

##### 產生Credentials 
[組態與登入資料檔案設定](https://docs.aws.amazon.com/zh_tw/cli/latest/userguide/cli-configure-files.html)
 Windows 中是使用環境變數 %UserProfile% (通常是c:/users/xxx)來參考，而在 Unix 系統中是使用 $HOME 或 ~ (波狀符號) 來參考
- 可以下載AWS CLI 來幫你產生這些檔案
- minIO server的產生方式可以看這篇[AWS CLI with MinIO Server](https://docs.min.io/docs/aws-cli-with-minio.html)

測試用aws CLI列出buckets
```shell 
>aws configure
AWS Access Key ID [****************MPLE]: Q3AM3UQ867SPQQA43P2F
AWS Secret Access Key [****************EKEY]: zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG
Default region name [us-east-1]:
Default output format [None]:

>aws configure set default.s3.signature_version s3v4

>aws --endpoint-url https://play.min.io s3 ls

2021-04-06 00:05:40 00dst1
2021-04-06 00:05:53 00dst2
(略)
```





## 網路參考文章
{% note warning %} <span style="font-size: 9px;">
學習路上感謝網路大神們，如果你發現了我，可以查看以下參考文章了解更多概念👇👇👇</span>{% endnote %}
- [amazon-s3開發是否有免費帳號](https://stackoverflow.com/questions/1375285/amazon-s3-developer-free-account-for-testing-purposes)
