## s3 object metadata
#### Activities
**Create a bucket**
aws s3 mb s3://metadata-bucket-12324234123

**Make a file with contents**
echo "Earth Planet" > planet_file.txt

**Copy file object with metadata  to s3**
aws s3api put-object \
    --bucket metadata-bucket-12324234123 \
    --key planet-file.txt \
    --body planet-file.txt \
    --metadata "planet=earth, population=8.025 billion"

**Get object metadata**
aws s3api head-object --bucket metadata-bucket-12324234123 --key planet-file.txt


#### Clean ups

**Empty bucket**
aws s3 rm s3://metadata-bucket-12324234123 --recursive

**delete bucket**
aws s3 rb s3://metadata-bucket-12324234123

