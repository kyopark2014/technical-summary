# CDK 소개

## CDK 정의

AWS CDK(Cloud Development Kit)는 프로그래밍 언어를 사용하여 클라우드 인프라를 코드로 정의하고, AWS CloudFormation을 통해 배포하는 오픈 소스 소프트웨어 개발 프레임워크입니다. Typescript, Node.JS, Python, Go와 같은 다양한 언어를 지원하므로 인프라를 쉽게 개발할 수 있습니다. 

CDK는 2018년 8월에 [AWS CDK Developer Preview](https://aws.amazon.com/ko/blogs/developer/aws-cdk-developer-preview/)에 처음 릴리즈 되었고, CDK v2는 [AWS Cloud Development Kit (AWS CDK) v2 is now generally available](https://aws.amazon.com/about-aws/whats-new/2021/12/aws-cloud-development-kit-cdk-generally-available/?nc1=h_ls)와 같이 2021년 11월에 정식 릴리즈 되었습니다.

기본적으로 CDK는 CloudFormation Template을 생성하기 위한 툴이므로, AWS에서 새로운 feature를 개발하였을때, 새로운 feature가 CloudFormation으로 개발된 후 다시 CDK 새버전이 배포될때까지 기다려야 할 수 있습니다. 또한, CDK for Teraform과 같이 CloudFormation이외에도 사용될 수 있도록 확장되고 있습니다. 

### CDK Initiation

Typescript로 cdk를 설정시 아래와 같이 합니다.

```c
$ cdk init app --language typescript

$ cdk bootstrap aws://123456789012/ap-northeast-2
```
여기서 '123456789012'은 Account Number를 의미합니다.

aws-cdk-lib를 수동으로 Upgrade를 해줍니다.

```c
$ npm install -g aws-cdk-lib
```


### AWS CDK Benefits

1) Easier cloud onboarding — AWS CDK accelerates your onboarding to AWS because there are few new things to learn. CDK enables you to use your existing skills and tools, and apply those to the task of building cloud infrastructure. It also provides high-level components that preconfigure cloud resources with proven defaults, helping you build on AWS without needing to be an expert.

2) Customisable and shareable — With AWS CDK you can design your own reusable components that meet your organisation’s security, compliance, and governance requirements. Just like with any other software library, you can easily share components around your organisation enabling you to rapidly bootstrap new projects with best practices by default.

3) Faster development process — AWS CDK gives you the expressive power of programming languages for defining infrastructure. Familiar features such as objects, loops, and conditions accelerate your development process. You can also use AWS CDK with your integrated development environment (IDE) to take advantage of existing productivity tools and testing frameworks.

4) No context switching — AWS CDK enables you to build your cloud application without leaving your IDE. You can write your runtime code and define your AWS resources with the same programming language. You can visualise your CDK application stacks and resources with the AWS Toolkit for VS Code.


### CDK Construct 

- Level 1 (L1) construct

These are direct representations of CloudFormation resources. When you choose L1 constructs you must provide all the required CloudFormation attributes for a particular cloud resource.

- Level 2 (L2) construct

A Level 2 construct also represents a particular cloud resource. E.g. An S3 bucket. But you don’t have to configure every configuration attribute. Instead, they are provided with convenient default values such that you can easily spin up a certain cloud resource.

- Level 3 (L3) construct

A Level 3 construct represents a bunch of cloud resources that work together to accomplish a particular task. They are also called “patterns”. For example, you can create an ApplicationLoadBalancedFarageteService which will create an ECS cluster powered by Fargate, an ECR repository to host your Docker images, Application Load Balancer to access your containers, etc…

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


## [AWS CDK와 AWS SAM은 어떤 관계](https://aws.amazon.com/ko/cdk/faqs/)

AWS Serverless Application Model 및 AWS CDK는 모두 AWS 인프라를 코드로 추상화하므로 클라우드 인프라를 더 쉽게 정의할 수 있습니다. AWS SAM은 서버리스 사용 사례와 아키텍처에 초점을 맞추고 있으며 인프라를 간결한 선언형 JSON/YAML 템플릿으로 정의할 수 있습니다. AWS CDK는 모든 AWS 서비스에 걸쳐 광범위한 지원을 제공하며 클라우드 인프라를 TypeScript, Python, C# 및 Java와 같은 현대적 프로그래밍 언어로 정의할 수 있습니다. AWS SAM 및 AWS CDK 모두 CloudFormation을 인프라 스택의 프로비저닝 엔진으로 활용합니다.

간결한 선언형 템플릿으로 서버리스 인프라를 정의하는 것을 선호한다면 SAM이 더 적합합니다. AWS 인프라를 익숙한 프로그래밍 언어로 정의하려는 경우에는 AWS CDK를 사용하는 것이 좋습니다. 두 경우 모두 CloudFormation을 통해 반복 가능하고 안전한 인프라 배포를 활용할 수 있습니다.


## Reference 

1) [What is the AWS CDK?](https://docs.aws.amazon.com/cdk/v2/guide/home.html)

2) [AWS CDK Benefits](https://medium.com/@kargawal.abhishek/aws-cdk-deploy-managed-etl-using-aws-glue-job-1925098ec40f)

3) [CDK for Terraform](https://www.terraform.io/cdktf)

4) [CDK for Kubernetes](https://cdk8s.io/)

5) [AWS Cloud Development Kit FAQ](https://aws.amazon.com/ko/cdk/faqs/)

6) [[AWS Builders] AWS Cloud Development Kit을 이용한 Code 기반의 인프라 구축](https://www.youtube.com/watch?v=hOJbhfF0DYQ)

7) [AWS CDK Developer Preview](https://aws.amazon.com/ko/blogs/developer/aws-cdk-developer-preview/)

8) [AWS CDK — A Beginner’s Guide with Examples](https://enlear.academy/aws-cdk-a-beginners-guide-with-examples-424c600ac409)
