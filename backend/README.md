# AWS API Gateway with a Mock Integration

## Validation

```bash
aws cloudformation validate-template \
--template-body template.yaml
```

## Deployment

```bash
sam build && 

sam deploy \
--stack-name mock-api \
--template-file template.yaml\
--capabilities CAPABILITY_IAM
--confirm-changeset
```

## Testing

```bash
API_GATEWAY_ID=$(aws apigateway get-rest-apis --query 'items[?name==`mock-api`].id' | grep -o -E "[a-z0-9]+")
```

You can a method test directly in the console


If you provision your own api, replace the api endpoint below during your request. You can find in the export when
you provision or modify your stack, or you can find it in the AWS console.

**Every time you make a change to the Api via Cloudformation, you need to re-deploy it in the console.**
Go to your api > Resources > Actions > Deploy Api > pick v0 stage > Deploy
It can take a few seconds for deploy to happen

```bash
curl --location --request GET 'https://7zd691nm88.execute-api.us-east-1.amazonaws.com/v0/data' \
--header 'Content-Type: application/json'
```