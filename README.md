# Custom Guardrail for AWS Glue Encryption using Event-driven Architecture

One of the great values AWS delivers to customers is the ability to conciliate agility and security, giving freedom to experimentation, new ideas, and business transformation in a secure and scalable way. Using this template, you can deploy a Custom Guardrail in your organization using Event-driven Architecture under services as Amazon EventBridge, AWS Lambda, AWS CloudTrail, AWS KMS, and AWS CloudFormation. 

For this use case, we want encryption to be enabled in AWS Glue. Therefore, the resulting Guardrail will be in charge of detecting and reacting to changes in the infrastructure to enforce compliance with the encryption mandate. The template creates all the resources required in our example, including Guardrail components and the initial desired configuration that activates encryption in AWS Glue. 

The flexibility to build your own unique Guardrail rules empowers your teams to meet any configuration and security baseline compliance requirements, establishing a solid foundation for your AWS environment. The approach demonstrated in this template offers excellent opportunities to improve your organization's security posture using Event-driven Architecture.

## Solution architecture and design
The following diagram illustrates the Custom Guardrails through Event-driven Architecture for AWS Glue Encryption Settings:

## ![](/Images/aws-architecture-custom-guardrail-event-driven.png)

The workflow and architecture of the solution works as follows:

1.	CloudFormation Template creates all the resources: Guardrails components and the initial desired configuration of encryption in AWS Glue;
2.	EventBridge Rule detects change in state of the encryption configuration;
3.	Lambda Function is invoked to evaluate and logging (CloudWatch Logs):
    - For non-compliant detection the SSM Parameter is recovered with KMS Arn 	
    - The service is remediated to compliant status with encryption enabled

## AWS Services and Resources that will be deployed:

- Amazon Event Bridge Rule
- AWS Lambda Function
- AWS IAM Managed Role
- AWS IAM Policy
- AWS SSM Parameter Store
- AWS KMS CMK
- AWS KMS Alias
- AWS CloudFormation Stack
- Amazon CloudWatch Logs (from AWS Lambda Executions)

## Custom Guardrail in Action

For firing up the custom guardrail and seeing it running, follow these steps:

1.	Run the available [CloudFormation Template](/CloudFormation/aws-custom-guardrail-event-driven.yaml) (no input parameters required) until you reach the status **CREATE_COMPLETE**: 
![](/Images/image-02.png)

2.  After the deployment you can check Glue Settings in the Console:
![](/Images/image-03.png)

3.	Still inside Glue Settings, uncheck “Metadata encryption” and “Encrypt connection passwords”, then click Save, effectively putting the provisioned infrastructure in an **uncompliant state**:
![](/Images/image-04.png)

4.	In a few seconds after you save that configuration change, the Custom Guardrail will detect Glue’s uncompliant state and **enforce policy compliance** by automatically remediating the encryption misconfiguration.

5.	Now, refresh Glue setting’s console page and notice that all encryption options that were once deactivated are now properly set as they should: 
![](/Images/image-05.png)

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the Apache License 2.0. See the LICENSE file.
