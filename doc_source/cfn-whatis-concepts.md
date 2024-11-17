# AWS CloudFormation concepts<a name="cfn-whatis-concepts"></a>

* AWS CloudFormation, main concepts
  * *templates*
  * *stacks*

**Topics**
+ [Templates](#cfn-concepts-templates)
+ [Stacks](#cfn-concepts-stacks)
+ [Change sets](#cfn-concepts-change-sets)

## Templates<a name="cfn-concepts-templates"></a>

* CloudFormation template
  * := text file / JSON or YAML formatted
    * allowed extensions
      * `.json`,
      * `.yaml`,
      * `.template`,
      * `.txt`
  * uses
    * 👀blueprints -- for -- building your AWS resources + their properties 👀
  * _Example:_ 

### JSON<a name="t2-micro-example.json"></a>

```
{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "A sample template",
    "Resources": {
        "MyEC2Instance": {
            "Type": "AWS::EC2::Instance",
            "Properties": {
                "ImageId": "ami-0ff8a91507f77f867",
                "InstanceType": "t2.micro",
                "KeyName": "testkey",
                "BlockDeviceMappings": [
                    {
                        "DeviceName": "/dev/sdm",
                        "Ebs": {
                            "VolumeType": "io1",
                            "Iops": 200,
                            "DeleteOnTermination": false,
                            "VolumeSize": 20
                        }
                    }
                ]
            }
        }
    }
}
```

### YAML<a name="t2-micro-example.yaml"></a>

```
AWSTemplateFormatVersion: 2010-09-09
Description: A sample template
Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: ami-0ff8a91507f77f867
      InstanceType: t2.micro
      KeyName: testkey
      BlockDeviceMappings:
        - DeviceName: /dev/sdm
          Ebs:
            VolumeType: io1
            Iops: 200
            DeleteOnTermination: false
            VolumeSize: 20
```

You can also specify multiple resources in a single template and configure these resources to work together\. For example, you can modify the previous template to include an Elastic IP address \(EIP\) and associate it with the Amazon EC2 instance, as shown in the following example:

### JSON<a name="multiple-resources-single-template.json"></a>

```
{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "A sample template",
    "Resources": {
        "MyEC2Instance": {
            "Type": "AWS::EC2::Instance",
            "Properties": {
                "ImageId": "ami-0ff8a91507f77f867",
                "InstanceType": "t2.micro",
                "KeyName": "testkey",
                "BlockDeviceMappings": [
                    {
                        "DeviceName": "/dev/sdm",
                        "Ebs": {
                            "VolumeType": "io1",
                            "Iops": 200,
                            "DeleteOnTermination": false,
                            "VolumeSize": 20
                        }
                    }
                ]
            }
        },
        "MyEIP": {
            "Type": "AWS::EC2::EIP",
            "Properties": {
                "InstanceId": {
                    "Ref": "MyEC2Instance"
                }
            }
        }
    }
}
```

### YAML<a name="multiple-resources-single-template.yaml"></a>

```
AWSTemplateFormatVersion: 2010-09-09
Description: A sample template
Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: ami-0ff8a91507f77f867
      InstanceType: t2.micro
      KeyName: testkey
      BlockDeviceMappings:
        - DeviceName: /dev/sdm
          Ebs:
            VolumeType: io1
            Iops: 200
            DeleteOnTermination: false
            VolumeSize: 20
  MyEIP:
    Type: 'AWS::EC2::EIP'
    Properties:
      InstanceId: !Ref MyEC2Instance
```

The previous templates are centered around a single Amazon EC2 instance; however, CloudFormation templates have additional capabilities that you can use to build complex sets of resources and reuse those templates in multiple contexts\. For example, you can add input parameters whose values are specified when you create a CloudFormation stack\. In other words, you can specify a value like the instance type when you create a stack instead of when you create the template, making the template easier to reuse in different situations\.

For more information about template creation and capabilities, see [Template anatomy](template-anatomy.md)\.

For more information about declaring specific resources, see [AWS resource and property types reference](aws-template-resource-type-ref.md)\.

To start designing your own templates with AWS CloudFormation Designer, go to [https://console\.aws\.amazon\.com/cloudformation/designer](https://console.aws.amazon.com/cloudformation/designer)\.

## Stacks<a name="cfn-concepts-stacks"></a>

* stack
  * 👀1! unit / == AWS resources
    * -- managed via -- CloudFormation👀
      * you create, update, and delete a collection of resources -- by -- creating, updating, and deleting stacks
    * -- defined by -- CloudFormation template
  * ⭐️if you submit the template -> you create a stack -> CloudFormation provisions the resources / described | your template ⭐️
  * ways to work with stacks
    * CloudFormation 
      * [console](https://console.aws.amazon.com/cloudformation/),
      * [API](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/),
    * [AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/cloudformation)
  * see [Working with stacks](stacks.md)

## Change sets<a name="cfn-concepts-change-sets"></a>

* Change sets
  * == summary of your proposed changes
    * use cases
      * making changes | stack's running resources & BEFORE making changes
  * allow
    * see how your changes -- might impact -- your running resources
  * see [Updating stacks using change sets](using-cfn-updating-stacks-changesets.md)