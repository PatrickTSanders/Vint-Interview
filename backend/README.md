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

```bash
curl --location --request GET 'https://7zd691nm88.execute-api.us-east-1.amazonaws.com/v0/data' \
--header 'Content-Type: application/json'
```