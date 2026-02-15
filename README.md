

  aws cloudformation create-change-set \
  --stack-name my-app-stack \
  --change-set-name import-bucket \
  --change-set-type IMPORT \
  --template-body file://import-template.yaml \
  --resources-to-import '[{
    "ResourceType": "AWS::S3::Bucket",
    "LogicalResourceId": "ImportedAppBucket",
    "ResourceIdentifier": {"BucketName": "appjerwo-demo-test"}
  }]' \
  --capabilities CAPABILITY_NAMED_IAM --region ap-southeast-2


aws cloudformation execute-change-set \
  --stack-name my-app-stack \
  --change-set-name import-bucket --region ap-southeast-2

# Standard update (NOT import!)

aws cloudformation deploy \
  --stack-name my-app-stack \
  --template-file full-stack.yaml \
  --capabilities CAPABILITY_NAMED_IAM --region ap-southeast-2  