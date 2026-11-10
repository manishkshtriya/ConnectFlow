# ConnectFlow — Cloud-Based Customer Contact Center

Portfolio project for a fictional bank support desk using Amazon Connect, AWS Lambda, DynamoDB and CloudWatch.

**Project status:** This repository will contain backend source, an AWS SAM template, unit tests, sample data and implementation guides. It is not yet a live contact centre. You must create/configure the Amazon Connect instance, phone number, contact flows, queues and agents in your AWS account, then test a real inbound call before describing it as deployed.

## Architecture

```text
Customer -> Amazon Connect -> IVR contact flow -> collect demo customer ID
                                      |
                                      v
                              CustomerLookup Lambda
                                      |
                                      v
                               DynamoDB profiles
                                      |
                                      v
                         Account / Card / General queue
                                      |
                                      v
                                  Connect agent
```

## Download the complete source package

[Download ConnectFlow source ZIP](./ConnectFlow_Source.zip) — includes the SAM template, Python Lambda functions, unit tests, sample data, and implementation guides.

After downloading, extract the ZIP and follow `docs/deployment-guide.md`.

## Included
- Customer lookup Lambda with input validation
- Call event logging Lambda
- DynamoDB tables for synthetic customer profiles and call records
- AWS SAM / CloudFormation deployment template
- Unit tests and sample Lambda event
- Contact-flow build guide, deployment instructions, testing checklist and security/cost notes

## Quick start
Requirements: Python 3.12, AWS CLI, AWS SAM CLI, and an AWS account.

```bash
python -m pip install boto3 botocore
python -m unittest discover -s tests -v
sam validate --lint
sam build
sam deploy --guided
```

The SAM stack deploys the backend resources. It does **not** create an Amazon Connect instance or purchase/claim a phone number. Follow `docs/deployment-guide.md` and `docs/contact-flow-build-guide.md`.

## Demo IDs
- CF1001 — Rahul Sharma — Account
- CF1002 — Asha Rao — Card
- CF1003 — Kiran Shetty — General

Use synthetic data only. Never store real banking credentials, card numbers, CVVs, PINs, passwords or OTPs.

## Current limitations
Amazon Connect instance, phone number, queues, routing profiles, agent users and visual contact flows must be configured in the Connect console. This repository is a deployable backend foundation plus a detailed console configuration guide; it is not evidence of a completed end-to-end call-centre deployment.
