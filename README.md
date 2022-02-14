# Application Performance Coding Challenge

### Packaged Applications
* AWS SNS + SQS using [localstack](https://github.com/localstack/localstack) version 0.12.19
* PostgreSQL DB version 14
* Payroll Service

### Pre Requisites
`Docker` and `docker-compose version 2+` should be installed

**Specifically for mac users**

`Docker` should have permission to the base directory where this package is downloaded inorder to mount the volumes

eg: If the package is downloaded into `Downloads` folder, docker should have access to `Downloads` folder

### How to run ?
* Execute the following command from the base directory which contains the `docker-compose.yaml` file
```
docker-compose up
```
It'll bring up the AWS SNS + SQS, a PostgreSQL DB and the Payroll service locally.

**Database Details**
```
Database name : performance
Table name : performance
Columns : id, company_id, occurred_at, processed_at

Username : postgres
Password : encryptedpassword
```

**SNS Details**
```
Topic ARN : arn:aws:sns:us-east-1:000000000000:local_sns
```

**Sample Event**
```
{
    "eventType": "employee.updated",
    "occurredAt": "2021-10-20T12:00:01.000Z",
    "companyId": "1000",
    "employeeId": "1",
    "attributes": {
      "firstName": "Bennet",
      "lastName": "Ben"
    }
  }
```

**Publishing Event using aws command line**

To configure aws command line run the following commands
```
export AWS_PROFILE=mylocalprofile
aws configure
```
* Enter `AWS Access Key ID` as `accesskey`
* Enter `AWS Secret Access Key` as `secretaccesskey`
* Enter `Default region name` as `us-east-1`
* Leave it as it is for `Default output format`

Execute the following to publish an event
```
aws --endpoint-url=http://localhost:4566 sns publish  --topic-arn arn:aws:sns:us-east-1:000000000000:local_sns --message '
  {
    "eventType": "employee.updated",
    "occurredAt": "2021-10-20T12:00:01.000Z",
    "companyId": "1000",
    "employeeId": "1",
    "attributes": {
      "firstName": "Bennet",
      "lastName": "Ben"
    }
  }
  '
```

**Note**: This entire solution has been tested in Mac OS.