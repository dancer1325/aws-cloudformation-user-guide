# How does AWS CloudFormation work?<a name="cfn-whatis-howdoesitwork"></a>

* | create stack -> AWS CloudFormation -- makes underlying service calls to -- AWS
  * / -- declared by -- CloudFormation template
  * to
    * provision your resources
      * 👀ONLY allowed the ones / you have permission 👀
        * managed -- via -- [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/) 
    * configure your resources

    ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/images/create-stack-diagram.png)

* steps
  1. create or use an existing CloudFormation template
     1. ways
        1. [AWS CloudFormation Designer](https://console.aws.amazon.com/cloudformation/designer) or
        2. your own text editor
     2. _Example:_ template to create an EC2 instance

        ```.json
        {
            "AWSTemplateFormatVersion": "2010-09-09",
            "Description": "A simple EC2 instance",
            "Resources": {
                "MyEC2Instance": {
                    "Type": "AWS::EC2::Instance",
                    "Properties": {
                        "ImageId": "ami-0ff8a91507f77f867",
                        "InstanceType": "t2.micro"
                    }
                }
            }
        }
        ```  

        ```.yaml
        AWSTemplateFormatVersion: 2010-09-09
        Description: A simple EC2 instance
        Resources:
         MyEC2Instance:
           Type: 'AWS::EC2::Instance'
           Properties:
             ImageId: ami-0ff8a91507f77f867
             InstanceType: t2.micro
        ```

  2. save the template |
     1. locally or
     2. Amazon S3 bucket

  3. create a CloudFormation stack -- specifying the -- location of your template file
     1. template's parameters -- can be passed as -- input values
     2. ways
        1. CloudFormation 
           1. [console](cfn-console-create-stack.md),
           2. [API](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_CreateStack.html),
        2. [AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/create-stack.html)
     3. if the template file is stored locally -> CloudFormation uploads it | AWS account's S3 bucket / EACH region | you upload a template file
        1. buckets -- are accessible to -- ANYONE / Amazon S3 permissions | your AWS account
        2. if a bucket created by CloudFormation is ALREADY present -> template added | that bucket
     4. CloudFormation provisions and configures resources -- by making calls to the -- AWS services
     5. if stack creation fails -> CloudFormation rolls back your changes -- by -- deleting the resources / it created

## Updating a stack with change sets<a name="updating-stack-with-change-sets"></a>

* TODO:
When you need to update your stack's resources, you can modify the stack's template\. You don't need to create a new stack and delete the old one\. To update a stack, create a change set by submitting a modified version of the original stack template, different input parameter values, or both\. CloudFormation compares the modified template with the original template and generates a change set\. The change set lists the proposed changes\. After reviewing the changes, you can start the change set to update your stack or you can create a new change set\. The following diagram summarizes the workflow for updating a stack\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/images/update-stack-diagram.png)

**Important**  
Updates can cause interruptions\. Depending on the resource and properties that you are updating, an update might interrupt or even replace an existing resource\. For more information, see [AWS CloudFormation stack updates](using-cfn-updating-stacks.md)\.

1. You can modify a CloudFormation stack template by using [AWS CloudFormation Designer](https://console.aws.amazon.com/cloudformation/designer) or a text editor\. For example, if you want to change the instance type for an EC2 instance, you would change the value of the `InstanceType` property in the original stack's template\.

   For more information, see [Modifying a stack template](using-cfn-updating-stacks-get-template.md)\.

1. Save the CloudFormation template locally or in an S3 bucket\.

1. Create a change set by specifying the stack that you want to update and the location of the modified template, such as a path on your local computer or an Amazon S3 URL\. If the template contains parameters, you can specify values when you create the change set\.

   For more information about creating change sets, see [Updating stacks using change sets](using-cfn-updating-stacks-changesets.md)\.
**Note**  
If you specify a template that's stored on your local computer, CloudFormation automatically uploads your template to an S3 bucket in your AWS account\.

1. View the change set to check that CloudFormation will perform the changes that you expect\. For example, check whether CloudFormation will replace any critical stack resources\. You can create as many change sets as you need until you have included the changes that you want\.
**Important**  
Change sets don't indicate whether your stack update will be successful\. For example, a change set doesn't check if you will surpass an account [quota](cloudformation-limits.md), if you're updating a [resource](aws-template-resource-type-ref.md) that doesn't support updates, or if you have insufficient [permissions](using-iam-template.md) to modify a resource, which can cause a stack update to fail\.

1. Initiate the change set that you want to apply to your stack\. CloudFormation updates your stack by updating only the resources that you modified and signals that your stack has been successfully updated\. If the stack updates fails, CloudFormation rolls back changes to restore the stack to the last known working state\.

## Deleting a stack<a name="how-to-delete-a-stack"></a>

When you delete a stack, you specify the stack to delete, and CloudFormation deletes the stack and all the resources in that stack\. You can delete stacks by using the CloudFormation [console](cfn-console-delete-stack.md), [API](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_DeleteStack.html), or [AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/delete-stack.html)\.

If you want to delete a stack but want to retain some resources in that stack, you can use a [deletion policy](aws-attribute-deletionpolicy.md) to retain those resources\.

After all the resources have been deleted, CloudFormation signals that your stack has been successfully deleted\. If CloudFormation can't delete a resource, the stack won't be deleted\. Any resources that haven't been deleted will remain until you can successfully delete the stack\.

## Additional resources<a name="what-is-cfn-additional-resource"></a>
+ For more information about creating CloudFormation templates, see [Template anatomy](template-anatomy.md)\.
+ For more information about creating, updating, or deleting stacks, see [Working with stacks](stacks.md)\.