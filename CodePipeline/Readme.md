# CodePipeline

Creation of an automated CI/CD pipeline which
1) builds a new _simplehttp_ container image
2) pushes the image to ECR
3) deploys the image to an ECS service

## extending the buildspec.yml
The deploy phase needs the information about
1. the which container needs to be updated, and
2. to which image it needs to be updated
This information needs to be created in the build phase and stored as artifact. This artifact is then used in the deploy phase to update the ECS service (in detail: its task definition).

Add the following  lines to the bottom of file _buildspec.yml_

!! The _name_ has to match the containername within the task definition of your service !!

```
      - printf '[{"name":"simplehttp-container","imageUri":"%s"}]' $REPOSITORY_URI:$IMAGE_TAG > imagedefinitions.json
artifacts:
    files: imagedefinitions.json
```

Save the file and push it to CodeCommit !

## create the CodePipeline pipeline

* let the wizard create a service role
* configure the _simplehttp_ repository as _Source_
* configure the _simplehttp-cb_ project as _Build_ source
* as _Deploy provider_ choose **Amazon ECS**
    * select the ECS cluster _ecs-ec2_
    * select the service we want to use, e.g. _simplehttp-from-ecr_
    * enter the _Image definitions file_, this is the file _imagedefinitions.json_, created by the build phase