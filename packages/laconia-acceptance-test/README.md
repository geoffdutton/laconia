# @laconia/acceptance-test

This test is running in the cloud try to cover most of high level features of
laconia by mimicking a real world application. To see what kind of interaction
is happening in between all the AWS resources, have a look into the
[architecture diagram](docs/architecture-diagram.drawio.png).

## Setup
First things first, decide what region you want to use and install the packages:
```bash
export AWS_REGION=us-west-2
npm i
```
*Note: There's a chance not all services are available in all regions.

Next, this app required an AWS SSM param in the format of `/[SERVICE_NAME]-[STAGE]/apiKey` (fill in SERVICE_NAME and STAGE with your own), and you need to set that to `supersecretkey`. You can do that in the console or via cli:

```bash
aws ssm put-parameter --name "/laconia-acceptance-node8/apikey" --value supersecretkey --type String --region us-west-2
```

Finally:
```bash
npm run deploy
# .... a bunch of output, and a few minutes later
npm test
# hopefully successful tests
npm run remove
```
