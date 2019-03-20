https://egghead.io/courses/develop-a-serverless-backend-using-node-js-on-aws-lambda

## AWS setup
## How to use aws cli
1. Add similar lines to your `.aws/credentials` using your cli acccount details. Name section as 
```
[qa-long-term]
region = eu-west-1
aws_access_key_id = ????
aws_secret_access_key = ?????
aws_mfa_device = arn:aws:iam::848569320300:mfa/nikita.panteleev_cli
```
2. Create short credentials using:
```
aws-mfa --profile qa
export AWS_PROFILE=qa
aws s3 ls
```

## How to install npm
```
brew install npm
npm install -g npm@latest
npm -v
```

Then libs:
```
npm i serverless -g
npm i serverless --save
```


## How to use serverless
`serverless.yml` defines setup
```
sls deploy
//or only redeploying the function
sls deploy function --function helloWorld
sls invoke --function helloWorld --log
```