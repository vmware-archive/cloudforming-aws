## Manual steps required

Before running CloudFormation, you'll have to create server certificates
for the ERT and Isolation Segments, as well as creating a key pair.

### Create and upload certs

#### ERT certs

1. create cert and key for ERT
2. upload it
```
aws iam upload-server-certificate --server-certificate-name pcf-env-id --certificate-body file://pcf-env-id.crt --private-key file://pcf-env-id.key
```

#### ISO certs

1. create cert and key for ISO
2. upload it
```
aws iam upload-server-certificate --server-certificate-name pcf-env-id-iso --certificate-body file://pcf-env-id-iso.crt --private-key file://pcf-env-id-iso.key
```

Then, get the ARNs and replace them in cloud formation template

### Create key pair

Make sure your AWS CLI is configured to point to the same region you
will be deploying your cloudformation.  Then, create a key pair:

```
aws ec2 create-key-pair --key-name pcf-env-id
```

(The key name should match what is in the template as `KeyName`)


