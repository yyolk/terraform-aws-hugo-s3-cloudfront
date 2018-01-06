# Terraform module for hosting Hugo sites on S3 and CloudFront

This module creates an S3 bucket with proper configuration to support Hugo's friendly urls. 
It also creates a CloudFront distribution with special S3 origin configuration to support S3 
redirects. S3 static websites can be accessed via three different hostname formats, but only one
supports S3 redirects. This module helps keep setup consistent for multiple Hugo sites. 

## Required Inputs 

 - `aliases` - A list of hostname aliases for CloudFront to listen on
 - `bucket_name` - Name of bucket to use, must be globally unique
 - `cert_domain` - Domain name on existing Amazon Certificate Manager certificate to use with CloudFront

## Optional Inputs

 - `aws_region` - The AWS region to create the S3 bucket in. Default: `us-east-1`
 - `cf_default_ttl` - Default CloudFront caching TTL. Default: `86400`
 - `cf_min_ttl` - Minimum CloudFront caching TTL. Default: `0`
 - `cf_max_ttl` - Maximum CloudFront caching TTL. Default: `31536000`
 - `cf_price_class` - The CloudFront pricing class to use. Default: `PriceClass_All`
 - `origin_path` - Path to document root in S3 bucket without slashes. Default: `public`
 
## Usage Example

```hcl
module "hugosite" {
  source      = "github.com/fillup/terraform-hugo-s3-cloudfront"
  aliases     = ["www.domain.com", "domain.com"]
  bucket_name = "www.domain.com"
  cert_domain = "*.domain.com"
}
```
    