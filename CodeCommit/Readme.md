# AWS CodeCommit

## Setup

### install Git

official docu for all OS'es: https://git-scm.com/download/linux

Ubuntu:  
```bash
sudo apt-get install git
```

### IAM permissions

attach the predefinex policy **_AWSCodeCommitPowerUser_** to your IAM user

### create git credentials

in the IAM section of AWS console,

* choose _Users_ ==> _your user_
* click tab _Security Credentials_
* in _HTTPS Git credentials for AWS CodeCommit_ click **_Generate_**

!! copy/save the username & password

### create repository

open the CodeCommit [page in AWS console](https://console.aws.amazon.com/codesuite/codecommit/home) , and click _create repository_, paste _simplehttp_ as name.    
Follow the _connection steps_ shown in the AWS console to clone the repository to your local workstation.

