## s3 Bucket Policy

#### Activities

##### Create a public bucket policy

**create a bucket**
aws s3 mb s3://public-bucket-policy-139823

**copy a file to s3**
echo "Public policy test file" > file.txt
aws s3 cp file.txt s3://public-bucket-policy-139823

**enable public access**
aws s3api put-public-access-block \
    --bucket public-bucket-policy-139823 \
    --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"

**insert bucket-policy to make files accessible to all**
aws s3api put-bucket-policy \
    --bucket public-bucket-policy-139823 \
    --policy file://policy.json

**confirm bucket policy is set**
aws s3api get-bucket-policy --bucket public-bucket-policy-139823

#### Create a cross account bucket policy

**create a bucket**
aws s3 mb s3://cross-account-bucket-policy-12134324

**cp file to bucket**
echo "cross acount bucket policy" > file2.txt
aws s3 cp file.txt s3://cross-account-bucket-policy-12134324/file2.txt

**enable public access**
aws s3api put-public-access-block \
    --bucket cross-account-bucket-policy-12134324 \
    --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"

**attach bucket policy**
aws s3api put-bucket-policy \
    --bucket cross-account-bucket-policy-12134324 \
    --policy file://cross-account-policy.json


**confirm bucket policy has been attached**
aws s3api get-bucket-policy --bucket cross-account-bucket-policy-12134324

**configure cli for aws another AWS account to access this bucket**
aws configure --profile muhammed

**test that you can list objects**
aws s3api list-objects --bucket cross-account-bucket-policy-12134324 --profile muhammed

**test that you can add objects**
echo "new file from another aws account" > new_file.txt
aws s3 cp new_file.txt s3://cross-account-bucket-policy-12134324 --profile muhammed

#### Clean Ups
** empty buckets**
aws s3 rm s3://public-bucket-policy-139823 --recursive 
aws s3 rm --recursive  s3://cross-account-bucket-policy-12134324

**delete buckests**
aws s3 rb s3://public-bucket-policy-139823
aws s3 rb s3://cross-account-bucket-policy-12134324


