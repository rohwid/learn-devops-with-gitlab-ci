# **What is DevOps?**

+ Not a standart or specification.
+ Not a tool or a particular software.
+ Not something you do with a tool of software.
+ DevOps is a cultural thing, it represents a change in mindset.

## **For Example of DevOps**

The usual business process is `Customter > Project Manager > Developer > Tester > SysAdmins`. Now, let's zoom in in Developers and SysAdmins and their main task:

For the Developer
+ Building software.
+ Adding new features.

For SysAdmins
+ Building and maintaining the IT infrastructure.
+ With the system run smoothly, securely, and with as little downtime.

Both of them, there are something in common, that's the `Software`.

For the SysAdmin
+ Knows very little about the software that need to operate.

For the developer
+ Knows very little of the infrastructure where the software is running.

Everyone in the business process work together on the software just in a different capacity, since the final outcome impact everyone it makesense for all these groups to collaborate. The cultural shift that DevOps brings is also tightly connected to the agile movement.

Where business conditions and requirements change all the time and where we need to juggle tons of tools and technology every day, the best culture is not one of blaming and finger-pointing but one of experimentation and learning from past mistakes. So, we want to have everyone collaborate instead of working in silos and stages or instead of finger pointing everyone takes responsibility for the final outcome. If the final product works and the customers or the users of the product are happy. So, the DevOps are:

+ More than just culture.
+ Focus on automating their tasks.
+ Because of manual and repetitive works is a productivity killer.

So, the main concern of this repository are **automatically building and deploying software which fall under a pactice called CI/CD**. We want to automate as much as possible to save time and give us the chance to put that time to good use instead of manually repeating the same task over and over again. But to automate things we need to get good at:

+ Using the **shell**.
+ Working with the **CLI tools**.
+ Reading documentation.
+ And writing scripts.

And here's the simple representation of DevOps.

<img src="img/devops.png" width="1000"/>

That proccess never stop, it goes on and on in an endless loop. It mean we contionue going through these steps with each iteration or new version of the software and get the **feedback** that add into the product. So, DevOps goes hand in hand with the agile movement.

# **GitLab CI/CD**

+ Automation engine.
+ Enables teams to perform DevOps pactices.
  + Continous Integration.
  + Continous Delivery/Deployment.
+ Automatically build, test, and deploy using GitLab pipeline.

# **GitLab Pipelines**

+ `.gitlab-ci.yml` from the root of the project repository.
+ Automated set of sequential steps to build, test, and deliver/deploy the code.
+ GitLab pipeline have two main components.
  + **Jobs** describe the tasks that need to be done.
  + **Stages** define the order in which jobs will be completed.
+ Set of instructions for a program to execute.
+ **Gitlab Runner** is the program that executes jobs in a GitLab pipeline.

## **GitLab Runner**

+ Separate program that can be run on **your local host**, **VM** or even **container**.
+ GitLab assigns pipeline jobs to available runners at pipeline runtime.

## **Main Feature of GitLab CI/CD**

+ Enter **CI/CD** menu and Select **Pipelines** and check the template example.
+ Or enter the **Editor** and select **Create new CI/CD pipelines**.
+ To check the visualiztion of CI/CD, check the **Visualize** tab.
+ To check the correct syntax, check the **Lint** tab.

## **What is CI/CD?**

### **CI (Continous Integration)**
+ There are steps for **build** and **test**, that called by Continous Integration.

### **CD (Continous Deployment)** 
+ After the CI process, continue to deploy in the staging server and continue to the production server.

### **CD (Continous Delivery)** 
+ After the CI process, continue to deploy in the staging server and taking action before deploy to the production server.

## **Setup Pipeline from Editor into the Visualize**

Here is the example of pipeline script in `.gitlab-ci.yml` that can edit from the Editor.

```
stages:          # List of stages for jobs, and their order of execution
  - build
  - test
  - deploy

build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - echo "Compiling the code..."
    - echo "Compile complete."

unit-test-job:   # This job runs in the test stage.
  stage: test    # It only starts when the job in the build stage completes successfully.
  script:
    - echo "Running unit tests... This will take about 60 seconds."
    - echo "Code coverage is 90%"

lint-test-job:   # This job also runs in the test stage.
  stage: test    # It can run at the same time as unit-test-job (in parallel).
  script:
    - echo "Linting code... This will take about 10 seconds."
    - echo "No lint issues found."

deploy-job:      # This job runs in the deploy stage.
  stage: deploy  # It only runs when *both* jobs in the test
   stage complete successfully.
  script:
    - echo "Deploying application..."
    - echo "Application successfully deployed."
```

Here are the main syntax of editor in the GitLab CI:

+ **`stages`**

    Inside the `stages`, there are:
    + `build`
    + `test`
    + `deploy`

The `stages` calls in every single CI/CD step like (for example from script above):
+ The `build-job` step has `build` stages.
+ The `unit-test-job` step has `test` stages.
+ The `lint-test-job` step has `test` stages.
+ The `deploy-job` step has `deploy` stages.

## **Docker Images**

Add docker images to execute the pipeline. It's like the environment where the CI/CD runs. Here's the config example:

```
image: python:latest
stages:                 # List of stages for jobs, and their order of execution
  - build
  - test
  - deploy
```

## **Pipeline Environment Variables**

Add variable that gonna use by the pipeline, you can describe it in the `.gitlab-ci.yml`. Here the example:

```
image: python:latest

variable:
  USERNAME: rohwid

stages:                 # List of stages for jobs, and their order of execution
  - build
  - test
  - deploy
```

Or define with the GitLab repository setting in `Settings > CI/CD > Variable > Collapse`. You can set the variable into two modes like:

+ **Protected**: Only can be use in the current protected branch.
+ **Masked**: Hide or encrypt the variable.

# **GitLab Runner**

+ Open source application that is used to run jobs in a GitLab CI/CD pipeline.
+ Pipeline jobs are assigned to available GitLab Runners.
+ The program can be installed on our local machine, VM, or Docker container and Cloud infrastructure.
+ Supported on Linux, Windows, macOS, and FreeBSD.
+ GitLab Runners execute the work defined in GitLab pipeline jobs (check the tasks on `script`).

  ```
  build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - echo "Compiling the code..."
    - echo "Compile complete."
  ```

## **GitLab Runner Types**

Here are the types of GitLab runner.

+ **Shared**: Available to all projects in a GitLab instance.
+ **Group**: Available to all projects in a group.
+ **Project**: For a single project or a set of project with specific requirements.

## **GitLab Runner Executor**

The GitLab Runner executor determines the environment in which a job will run.
+ In a VM vua a hypervisor such as VirtualBox
+ Shell
+ Remote SSH
+ Docker
+ Kubernetes
+ Custom executor (for environment that not supported by GitLab runner environment)

## **GitLab Runner Monitoring**

The runner program has an embedded Prometheus metric HTTP server for monitoring
+ Runner bussiness logic metrics
+ Go-specific process metrics
+ General process metrics
+ Build version information

## **Tags**

What is tags in GitLab CI/CD pipeline:
+ Tags can be added to a GitLab runner that can be reference in GitLab pipeline.
+ Reference tags from within a GitLab pipeline to **specify which runners should be used for a job**.
+ More explanation in the [docs](https://docs.gitlab.com/ee/ci/yaml/#tags).

## **Self-hosted Runners**

Why self-host runners?
+ Save on costs by using self-managed/hosted runners
+ Customization
+ Security

## **Steps for Self-hosting**

Here are the steps:
+ Install runner program on target host.
+ Choose an executor.
+ Register GitLab runner.
+ Run a pipeline that utilizes your runner.

## **Pre-requisites**

Before use GitLab pipeline we needs:
+ GitLab account.
+ VM or other infrastructure.
  + In this example: I'll be using a Linux machine as the GitLab Runner's host.
+ GitLab project.
+ Docker installed on target host where GitLab Runner will be installed.


Define the GitLab runners in GitLab repository setting in `Settings > CI/CD > Variable > Collapse`. There are two runners there are:

+ **Specific Runners**: Setup runners for the specific project on our local machinge, VM, or Docker container.
+ **Shared Runners**: Use the runners that provide by GitLab.

## **Setup Runners**

Setup GitLab runner on VM

## **GitLab CI/CD Cache**

Check the [docs](https://docs.gitlab.com/ee/ci/caching/) to setup the cache.

# **Step by Step GitLab CI**

+ Create the repository `try-gitlab-ci`.
+ Create `.gitlab-ci.yml` file and commit.
+ Create and define the stages.

    ```
    stages:
      - build
      - test
      - ship
    ```

    And call all the stages in every pipeline job. So, the script will be like this:
    
    ```
    ...
    
    build-job:
    stage: build
    script:
        - mkdir build
        - touch build/computer.txt
        - echo "Build the computer..."
        - echo "- CPU" >> build/computer.txt
        - echo "- Mainboard" >> build/computer.txt
        - echo "- RAM" >> build/computer.txt
        - echo "- SSD" >> build/computer.txt
        - echo "- Monitor" >> build/computer.txt
        - echo "- Keyboard" >> build/computer.txt
        - echo "- Mouse" >> build/computer.txt
        - echo "Build complete."

    test-job:
    stage: test
    script:
        - echo "Checking the components... This will take about 10 seconds."
        - test -f build/computer.txt 
        - cat build/computer.txt

    ship-job:
    stage: ship
    script:
        - echo "shiping the computer..."
        - mkdir ship
        - cp build/computer.txt ship
        - echo "The computer successfully shiped."
        - cat ship/computer.txt
    ```

+ Setup the artifacts paths.

    ```
    artifacts:
        paths:
        - build
    ```
    And call the artifact path in the pipeline job that needed. So, the script will be like this:

    ```
    ...

    build-job:
    stage: build
    script:
        - ls
        - mkdir build
        - touch build/computer.txt
        - echo "Build the computer..."
        - echo "- CPU" >> build/computer.txt
        - echo "- Mainboard" >> build/computer.txt
        - echo "- RAM" >> build/computer.txt
        - echo "- SSD" >> build/computer.txt
        - echo "- Monitor" >> build/computer.txt
        - echo "- Keyboard" >> build/computer.txt
        - echo "- Mouse" >> build/computer.txt
        - echo "Build complete."
    artifacts:
        paths:
        - build

    ...
    ```

+ Setup the variables.

    ```
    variables:
        BUILD_FILE_NAME: computer.txt
    ```

    And replace some config with variables name.

+ Set the GitLab **Setting** in **General**:

  + Use **Fast-forward merge** method.
  + **Squash commit when mergin** into **Encourage**.
  + **Merge checks** when **Pipelines must succeed**.

+ Set the GitLab **Setting** in **Repository**:
  
  + **Allowed to push** into **No one**.

+ That setting allow us to manage the repository easier, just the `main` branch and the **deployed version**.

<img src="img/github-semantic-branches.svg" width="1000"/>

# **Setup CI/CD for the Project that Runs in Background**

Here the example of the stages that we do previously:
  + Build in the `build` stage (ex: `build website` or `build-job`).
  + linter test in the `test` stage (ex: `linter` or `linter-test-job`).
  + Unit test in the `test` stage (ex: `unit test` or `unit-test-job`).

And here the `stages`, that what we will do.

```
stages:
  - build
  - test
  - deploy production
  - test production
 ```

Now we will do website test stage (ex: `test website` or `test-website-job`). For example, this is a backend program that runs in `http://localhost:3000`.

+ Add `&` parameter in the end running program. For example:

  ```
  python endpoint.py &
  ```

+ Add the delay after the program execution, because of the `curl` will execute imediately after the program execute and didn't make sure the program running well or not.

  ```
  sleep 10
  ```

+ Test the output with `curl`. For example:

  ```
  curl http://localhost:5000 | grep  "data"
  ```

  So, the complete stage will be like this:

  ```
  test website:
    image: python:latest
    stage: test
    script:
      - pip install -r requirements.txt
      - apt install curl -y
      - python endpoint.py &
      - sleep 10
      - curl http://localhost:5000 | grep "Flask App"
  ```

+ AWS CLI in pipeline, this is example how to gonna use AWS CLI in Gitlab CI pipeline.
  
  ```
  deploy to production:
    stage: deploy production
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    script:
      - aws --version
  ```

+ Masking and protecting the variables, this part already explained in **Pipeline Environment Variables** section. So, you don't need to write the variable in `.gitlab-ci.yml`, you just need to call the variable like this example:

  ```
  deploy to production:
    stage: deploy production
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    script:
      - aws --version
      - echo "Hello S3" > test.txt
      - aws s3 cp test.txt s3://$AWS_S3_BUCKET/test.txt
  ```

+ Add the AWS credential in **Pipeline Environment Variables** like this:
  + `AWS_S3_BUCKET` and disable protected branches.
  + `AWS_ACCESS_KEY_ID` and disable protected branches.
  + `AWS_SECRET_ACCESS_KEY` then disable the protected branches and masked the value.
  + `AWS_DEFAULT_REGION` and disable protected branches.

+ Upload multiple files into AWS S3 and delete it with `sync` command from AWS CLI.

  ```
  deploy to production:
    stage: deploy production
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    script:
      - aws --version
      - echo "Hello S3" > test.txt
      - aws s3 sync build/ s3://$AWS_S3_BUCKET --delete
  ```

+ Static website hosting on AWS S3 (So.. WOW).
  + Access and edit in menu **S3 > Properties > Static Website Hosting** and **Enable**.
  + Set the index document and error document.
  + Now enter again into the `Static Website Hosting`. There a website static hosting URL but it still can't be access if you click on it.
  + Go to `permission` tab and disable all the **Block Public Access** and **Edit** the **Bucket Policy** .
    + Search and add the bucket action to `GetObject` (for example: `"S3:GetObject"`).
    + Change the `Sid` value into `PublicRead` (for example: `"Sid": "PublicRead"`).
    + Change the `Principal` value into `*` (for example: `"Principal": "*"`).
    + Chenge the `Effect` value into `Allow` (for example: `"Effect": "Allow"`).
    + Change the `Resource` value into **aws bucket name** (for example: `"Resource": "arn:aws:s3:::(aws-s3-bucket-name)/*"`).
    + Now, you can access the static web hosting with AWS S3.
  
+ Add the `rules` params in `.gitlab-ci.yml` with this script and fill it with [**Predefined variable refference**](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html). So, it gonna make the currnet pipeline state will only execute in the main branch.

  ```
  rules:
      - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
  ```

  So, in the GitLab config:

  ```
  deploy to production:
    stage: deploy production
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    rules:
      - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
    script:
      - aws --version
      - echo "Hello S3" > test.txt
      - aws s3 sync build/ s3://$AWS_S3_BUCKET --delete
  ```

+ After deployed to the production, then add the `production test`. Before it, please define the `variables` like mentioned in **Pipeline Environment Variables** and add the **AWS S3 Static Web Hosting**.

  + Here is the variable example:

    ```
    variables:
      APP_BASE_URL: http://(aws-s3-static-web-hosting-url)
    ```

  + Now create the `production test` in the `post deploy` stages.

    ```
    production tests:
      image: curlimages/curl
      stage: test production
      rules:
        - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
      script:
        - curl $APP_BASE_URL | grep "Flask App"
    ```

+ Add the staging server to deploy.
  + Add new stage that named `deploy staging` and `test staging`.

    ```
    stages:
      - build
      - test
      - deploy staging
      - test staging
      - deploy production
      - test production
    ```

  + Copy the production stage and change it into staging.

    ```
    deploy to staging:
      stage: deploy staging
      image:
        name: amazon/aws-cli:2.4.11
        entrypoint: [""]
      rules:
        - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
      script:
        - aws --version
        - echo "Hello S3" > test.txt
        - aws s3 sync build/ s3://$AWS_S3_BUCKET_STAGING --delete
    ```

    And for the testing in staging.

    ```
    staging tests:
      image: curlimages/curl
      stage: test staging
      rules:
        - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
      script:
        - curl $APP_BASE_URL | grep "Flask App"
    ```

  + And here is the variable should be:

    ```
    variables:
      APP_BASE_URL: http://(aws-s3-production-static-web-hosting-url)
      APP_BASE_URL_STAGING: http://(aws-s3-staging-static-web-hosting-url)
    ```

## **Environment**

To enable this feature, enter the GitLab menu in `Deployments > Environments > New environment`.
+ Create the `staging` environment with the `staging` name and fill the external URL: `http://(aws-s3-staging-static-web-hosting-url)`.
+ Create the `production` environment with the `production` name and fill the external URL: `http://(aws-s3-production-static-web-hosting-url)`.
+ Now, remove the variables from `.gilab-ci.yml`.

  ```
  variables:
    APP_BASE_URL: http://(aws-s3-production-static-web-hosting-url)
    APP_BASE_URL_STAGING: http://(aws-s3-staging-static-web-hosting-url)
  ```
+ Go to **Setting > CI/CD**
  + Then set the **Variable** into specific **Environment scope** that defined before (`staging` and `production`).
  + `AWS_S3_BUCKET` into `production`.
  + rename `AWS_S3_BUCKET_STAGING` into `AWS_S3_BUCKET` into `staging`.

+ Modify the stage that define before by deleting the `test staging` and `test production` stages. So, the left stages will be like this.

  ```
  stages:
    - build
    - test
    - deploy staging
    - deploy production
  ```

+ Modify the `deploy staging` stage by combining with the `test staging` stage and change the `$APP_BASE_URL` variable into `$CI_ENVIRONMENT_URL` that provide by GitLab on [**Predefined variable refference**](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html) and don't forget to add `environment` variable with `staging` value.

  ```
  deploy to staging:
    stage: deploy staging
    environment: staging
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    rules:
      - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
    script:
      - aws --version
      - echo "Hello S3" > test.txt
      - aws s3 sync build/ s3://$AWS_S3_BUCKET --delete
      - curl $CI_ENVIRONMENT_URL | grep "Flask App"
  ```

+ Modify the `deploy production` stage by combining with the `test production` stage and change the `$AWS_S3_BUCKET_STAGING` variable into `$CI_ENVIRONMENT_URL` that provide by GitLab [**Predefined variable refference**](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html) and don't forget to add `environment` variable with `production` value.

  ```
  deploy to production:
    stage: deploy production
    environment: production
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    rules:
      - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
    script:
      - aws --version
      - echo "Hello S3" > test.txt
      - aws s3 sync build/ s3://$CI_ENVIRONMENT_URL --delete
      - curl $CI_ENVIRONMENT_URL | grep "Flask App"
  ```

## **Reusing Configuration**

Here are the steps to reusing the configuration.

+ Create new stage to reuse the `deploy staging` and the `deploy production`, because that two stages were identical. Don't forget to add `.` in front of the new stages, it means that stages are disabled.

  ```
  .deploy:
    image:
      name: amazon/aws-cli:2.4.11
      entrypoint: [""]
    rules:
      - if: $CLI_COMMIT_REF_NAME == $CI_DEFAULT_BRANCH
    script:
      - aws --version
      - echo "Hello S3" > test.txt
      - aws s3 sync build/ s3://$CI_ENVIRONMENT_URL --delete
      - curl $CI_ENVIRONMENT_URL | grep "Flask App"
  ```

+ Now, change the value of the `deploy to staging` and the `deploy to production`.

  For the `deploy to staging`:

  ```
  deploy to staging:
    stage: deploy staging
    environment: staging
    extends: .deploy
  ```

  For the `deploy to production`:

  ```
  deploy to production:
    stage: deploy production
    environment: production
    extends: .deploy
  ```