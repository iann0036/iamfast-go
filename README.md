<p align="center"><a href="https://github.com/iann0036/iamfast-js">JavaScript</a> • <a href="https://github.com/iann0036/iamfast-python">Python</a> • <b>Go</b> • <a href="https://github.com/iann0036/iamfast-java">Java</a> • <a href="https://github.com/iann0036/iamfast-vscode">VS Code</a></p>

# iamfast (Go)

:construction: EXPERIMENTAL - WORK IN PROGRESS :construction:

> IAM policy generation from application code

## Usage

```
cd go
go build -o iamfast
./iamfast yourfile.go
```

## Example

```
% cat go/tests/test1.go
package main

import (
	"github.com/aws/aws-sdk-go/aws"
	"github.com/aws/aws-sdk-go/aws/session"
	"github.com/aws/aws-sdk-go/service/s3"
)

func main() {
	sess, err := session.NewSession(&aws.Config{
		Region: aws.String("us-west-2")},
	)

	// Create S3 service client
	svc := s3.New(sess)

	// Create the S3 Bucket
	_, err = svc.CreateBucket(&s3.CreateBucketInput{
		Bucket: aws.String("abucket"),
	})
	if err != nil {
		panic(err)
	}
}
```

```
% cd go
% go build -o iamfast
% ./iamfast tests/test1.go
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:CreateBucket",
            "Resource": [
                "*"
            ]
        }
    ]
}
```
