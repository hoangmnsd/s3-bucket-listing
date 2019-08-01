# How to implement this:

1. Create s3 bucket name `example.bucket`
2. Edit `index.html` 2 lines:
```
  var S3BL_IGNORE_PATH = false;
  var BUCKET_URL = 'https://example.bucket.s3-ap-northeast-1.amazonaws.com';
```
3. Upload `index.html` and `list.js` to s3 bucket
4. Tab `Permission`, select `Block public access`, Edit, Uncheck to turn off.
5. Tab `Permission`, select `Access Control List`, select `Public access`, Grant everyone to `List Object` and `Read bucket permissions`
6. Tab `Permission`, select `Bucket Policy`, edit following code then paste and Save:
    (Note that you must change `example.bucket` to your own bucket name)
```
 {
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::example.bucket/*"
        }
    ]
}
```
7. Tab `Permission`, select `CORS configuration`, paste following code then Save:
```
<CORSConfiguration>
 <CORSRule>
   <AllowedOrigin>*</AllowedOrigin>
   <AllowedMethod>GET</AllowedMethod>
   <AllowedHeader>*</AllowedHeader>
 </CORSRule>
</CORSConfiguration>
```
8. Select tab `Properties`, select `Static website hosting`, select `Use this to host website`,
paste `index.html` to "Index document" and "Error document", save.

9. Access to Endpoint : http://example.bucket.s3-website-ap-northeast-1.amazonaws.com

Done!