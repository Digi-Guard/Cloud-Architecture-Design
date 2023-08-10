# AWS Network Architecture Diagram

## AWS Account Setup
- IAM Users: User1, User2
  - Permissions:
    - User1: Limited access to specific resources
    - User2: Limited access to specific resources
- IAM User Groups: AdminGroup, DevGroup
  - Permissions:
    - AdminGroup: Full administrative access
    - DevGroup: Access to development resources
- IAM Roles: GuardDutyRole, CloudTrailRole
  - Permissions:
    - GuardDutyRole: Permissions required for GuardDuty
    - CloudTrailRole: Permissions required for CloudTrail
- CloudFormation Stack: AutomationStack
  - Permissions: Necessary permissions for CloudFormation operations

## Security & Monitoring
- AWS GuardDuty: Monitors for suspicious activities and threats across the AWS environment.
  - Role: GuardDutyRole is assumed to grant necessary permissions for GuardDuty.
- AWS CloudTrail: Records API calls and provides an audit trail of account activity.
  - Role: CloudTrailRole is assumed to grant necessary permissions for CloudTrail.
- AWS CloudWatch: Collects and monitors metrics, generates alarms for various resources.
- Amazon SNS: Sends email alerts for CloudWatch alarms.

## Automation
- CloudFormation: Defines infrastructure as code, automates resource creation.
  - AutomationStack: Manages the creation and setup of various resources.

## Storage
- Amazon S3: Object storage service for storing logs and other data.
  - S3 Bucket: LogsBucket stores CloudTrail logs, VPC Flow Logs, and other data.

## Virtual Private Cloud (VPC)
- VPC: Isolated network environment to launch AWS resources.
  - CIDR Block: 10.0.0.0/16
  - Subnets:
    - PublicSubnet: 10.0.1.0/24
    - PrivateSubnet: 10.0.2.0/24
  - Flow Logs: Captures IP traffic flow for VPC monitoring.

## Virtual Private Cloud (VPC)
| Component            | CIDR Block     |
|----------------------|----------------|
| VPC                  | 10.0.0.0/16    |
| Public Subnet        | 10.0.1.0/24    |
| Private Subnet       | 10.0.2.0/24    |

## VPC Components
| Component            | Purpose                                             |
|----------------------|-----------------------------------------------------|
| Internet Gateway     | Provides internet access to resources in the VPC.  |
| NAT Gateway          | Enables outbound internet access for PrivateSubnet. |
| Customer Gateway     | Represents the on-premises VPN device.              |
| Virtual Private GW   | Attaches to VPC, provides entry/exit point for VPN.|

## EC2 Instances
- Public Subnet:
  - Linux Server EC2 Instance:
    - Security Group: Allows SSH (22) and HTTP (80) traffic.
    - Private IP: 10.0.1.10
- Private Subnet:
  - Windows Server EC2 Instance:
    - Security Group: Allows RDP (3389) traffic.
    - Private IP: 10.0.2.20
    - NAT Gateway: Enables outbound internet access for PrivateSubnet.
      - Elastic IP: 52.0.0.1

## VPN
- VPN Connection: Securely connects on-premises network to VPC.
  - Customer Gateway: Specifies on-premises VPN device's public IP.
  - Virtual Private Gateway: Attaches to VPC, provides entry/exit point.