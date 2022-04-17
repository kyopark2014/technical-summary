# CDK Introduction

## CDK 정의

AWS CDK(Cloud Development Kit)는 프로그래밍 언어를 사용하여 클라우드 인프라를 코드로 정의하고, AWS CloudFormation을 통해 배포하는 오픈 소스 소프트웨어 개발 프레임워크입니다. Typescript, Node.JS, Python, Go를 지원하므로 인프라를 쉽게 개발할 수 있습니다. 기본적으로 CDK는 CloudFormation을 생성하기 위한 툴이므로, AWS에서 새로운 feature를 개발하였을때, 새로운 feature가 CloudFormation으로 개발된 후 다시 CDK 새버전이 배포될때까지 기다려야하는 문제가 있습니다. 또한, CDK for Teraform과 같이 CloudFormation이외에도 사용될 수 있도록 확장되고 있습니다. 

### AWS CDK Benefits

1) Easier cloud onboarding — AWS CDK accelerates your onboarding to AWS because there are few new things to learn. CDK enables you to use your existing skills and tools, and apply those to the task of building cloud infrastructure. It also provides high-level components that preconfigure cloud resources with proven defaults, helping you build on AWS without needing to be an expert.

2) Customisable and shareable — With AWS CDK you can design your own reusable components that meet your organisation’s security, compliance, and governance requirements. Just like with any other software library, you can easily share components around your organisation enabling you to rapidly bootstrap new projects with best practices by default.

3) Faster development process — AWS CDK gives you the expressive power of programming languages for defining infrastructure. Familiar features such as objects, loops, and conditions accelerate your development process. You can also use AWS CDK with your integrated development environment (IDE) to take advantage of existing productivity tools and testing frameworks.

4) No context switching — AWS CDK enables you to build your cloud application without leaving your IDE. You can write your runtime code and define your AWS resources with the same programming language. You can visualise your CDK application stacks and resources with the AWS Toolkit for VS Code.


### 지원언어

. TypeScript, JavaScript, Python, Java, Go, C#/NET

![image](https://user-images.githubusercontent.com/52392004/163694512-ee73965c-8845-41dd-ad3b-fd77f2a243e2.png) (Reference #1)


## CDK v1/v2 차이

![image](https://user-images.githubusercontent.com/52392004/163694561-6ce0046d-024f-4328-9f19-ccb063faeb53.png)


![image](https://user-images.githubusercontent.com/52392004/163694564-2fd84efe-efe9-43a8-8691-15a56c93c858.png)


![image](https://user-images.githubusercontent.com/52392004/163694570-9a63faf3-ba50-433f-88bf-669fc240d5ab.png)


## CDK와 CloudFormation의 차이

![image](https://user-images.githubusercontent.com/52392004/163694615-e52d00d3-fa28-47f2-ad02-c1102ca90666.png)


## CDK for Teraform

HashiCorp Configuration Language (HCL)을 CDK를 이용해 구현합니다.

지원언어: TypeScript, Python, Java, C#, and Go (experimental).

![image](https://user-images.githubusercontent.com/52392004/163694803-b729a60f-59b8-4a2b-83a4-0cc454418ce1.png)

[설치 및 데모](https://learn.hashicorp.com/tutorials/terraform/cdktf-install?in=terraform/cdktf)


## CDK for Kubernetes (cdk8s)

cdk8s is a Cloud Native Computing Foundation Sandbox Project

cdk8s is an open-source software development framework for defining Kubernetes applications and reusable abstractions using familiar programming languages and rich object-oriented APIs. cdk8s apps synthesize into standard Kubernetes manifests which can be applied to any Kubernetes cluster.



## Reference 

1) [What is the AWS CDK?](https://docs.aws.amazon.com/cdk/v2/guide/home.html)

2) [AWS CDK Benefits](https://medium.com/@kargawal.abhishek/aws-cdk-deploy-managed-etl-using-aws-glue-job-1925098ec40f)

3) [CDK for Terraform](https://www.terraform.io/cdktf)

4) [CDK for Kubernetes](https://cdk8s.io/)

5) [AWS Cloud Development Kit FAQ](https://aws.amazon.com/ko/cdk/faqs/)
