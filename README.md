## Manual steps required

Before running CloudFormation, you'll have to create server certificates
for the ERT and Isolation Segments, as well as creating a key pair.

These will be input as parameters when you create the stack using the CloudFormation template.

Set or replace `${pcf-env-id}` with some prefix of your choosing.

### Create and upload certs

#### ERT certs

1. create cert and key for ERT
2. upload it
```
aws iam upload-server-certificate --server-certificate-name ${pcf-env-id} --certificate-body file://${pcf-env-id}.crt --private-key file://${pcf-env-id}.key
```

#### ISO certs

1. create cert and key for ISO
2. upload it
```
aws iam upload-server-certificate --server-certificate-name ${pcf-env-id}-iso --certificate-body file://${pcf-env-id}-iso.crt --private-key file://${pcf-env-id}-iso.key
```

Then, get the ARNs and replace them in cloud formation template

### Create key pair

Make sure your AWS CLI is configured to point to the same region you
will be deploying your cloudformation.  Then, create a key pair:

```
aws ec2 create-key-pair --key-name ${pcf-env-id}
```

### Hosted zones

The `hosted-zones.json` template can be used to configure DNS after the initial pcf stack
is created with `pcf-cloudformation.json`. It's helpful for testing, but is not part
of the official product release.
