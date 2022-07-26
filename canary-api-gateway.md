# Canary Deployment in API Gateway

## Canary Deployment

[Set up an API Gateway canary release deployment](https://docs.aws.amazon.com/apigateway/latest/developerguide/canary-release.html)

Canary release is a software development strategy in which a new version of an API (as well as other software) is deployed for testing purposes, and the base version remains deployed as a production release for normal operations on the same stage. For purposes of discussion, we refer to the base version as a production release in this documentation. Although this is reasonable, you are free to apply canary release on any non-production version for testing.


## CDK

A [percentage of API traffic](https://docs.aws.amazon.com/apigateway/latest/api/API_Stage.html#percentTraffic), between 0.0 and 100.0 inclusive, for the canary release.

[CanarySettings](https://docs.aws.amazon.com/apigateway/latest/api/API_CanarySettings.html)

![image](https://user-images.githubusercontent.com/52392004/180937260-0418a3f4-395c-485f-b25c-76ffa3f18d10.png)


[CanarySettingProperty](https://docs.aws.amazon.com/cdk/api/v1/docs/@aws-cdk_aws-apigateway.CfnDeployment.CanarySettingProperty.html)

```java
// The code below shows an example of how to instantiate this type.
// The values are placeholders you should change.
import * as apigateway from '@aws-cdk/aws-apigateway';
const canarySettingProperty: apigateway.CfnDeployment.CanarySettingProperty = {
  percentTraffic: 123,
  stageVariableOverrides: {
    stageVariableOverridesKey: 'stageVariableOverrides',
  },
  useStageCache: false,
};
```

### Properties

![image](https://user-images.githubusercontent.com/52392004/180937568-ed9c2535-7e2b-4c6a-9b15-a2efb127a7d6.png)

