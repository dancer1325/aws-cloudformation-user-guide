# What is AWS CloudFormation?<a name="Welcome"></a>

* AWS CloudFormation
  * allows
    * model & set up your AWS resources ->
      * you spend LESS time managing those resources
      * you focus on your applications / run | AWS
  * how does it work?
    * 👀you create a template / describes ALL the AWS resources / you want 👀
    * CloudFormation -- takes care of --
      * provisioning those resources
      * configuring those resources

## Simplify infrastructure management<a name="welcome-simplify-infrastructure-management"></a>

* | scalable web application / includes a backend database -> you might use
  * Auto Scaling group,
  * Elastic Load Balancing load balancer,
  * Amazon Relational Database Service database instance

* CloudFormation template
  * see [concepts](cfn-whatis-concepts.md#templatesa-namecfn-concepts-templatesa) 
* CloudFormation stack
  * see [concepts](cfn-whatis-concepts.md#stacksa-namecfn-concepts-stacksa)

## Quickly replicate your infrastructure<a name="welcome-quickly-replicate-your-infrastructure"></a>

* use cases
  * your application requires additional availability
* allows
  * if 1 region becomes unavailable -> your users can still use your application | OTHER regions
* requirements | replicating your application
  * replicate your resources == record ALL the resources + (provision + configure) / EACH region
    * resources / your application requires
* steps -- via -- CloudFormation
  * reuse your template,
  * provision the same resources | OTHER regions

## Easily control and track changes to your infrastructure<a name="welcome-easily-control-and-trach-changes"></a>

* _Example of use cases:_
  * change to a higher performing instance type
* if you provision manually -> you need to remember (for possible required roll back)
  * resources were changed,
  * original settings
* CloudFormation
  * track differences | CloudFormation template
    * _Example:_ version control system of your CloudFormation templates

## Related information<a name="welcome-related-information"></a>
+ see [AWS CloudFormation concepts](cfn-whatis-concepts.md)
+ see [How does AWS CloudFormation work?](cfn-whatis-howdoesitwork.md)
+ see [AWS CloudFormation pricing](http://aws.amazon.com/cloudformation/pricing/)