# react-native-docker

Continous Integration (CI) for Android apps on GitLab / Bitbucket
An image for building Android apps with support for multiple SDK Build Tools. This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool. Based on jangrewe/gitlab-ci-android.

Available images
javiersantos/android-ci:latest
image: javiersantos/android-ci:latest
Includes the latest SDK Build Tools and SDK Platform.

Build Tools: 28.0.3
Platform: Android 25, 26, 27 & 28
javiersantos/android-ci:28.0.3
image: javiersantos/android-ci:28.0.3
Build Tools: 28.0.3
Platform: Android 25, 26, 27 & 28
javiersantos/android-ci:28.0.2
image: javiersantos/android-ci:28.0.2
Build Tools: 28.0.2
Platform: Android 25, 26, 27 & 28
javiersantos/android-ci:27.0.3
image: javiersantos/android-ci:27.0.3
Build Tools: 27.0.3
Platform: Android 25, 26 & 27
javiersantos/android-ci:27.0.2
image: javiersantos/android-ci:27.0.2
Build Tools: 27.0.2
Platform: Android 25, 26 & 27
javiersantos/android-ci:27.0.1
image: javiersantos/android-ci:27.0.1
Build Tools: 27.0.1
Platform: Android 25, 26 & 27
javiersantos/android-ci:27.0.0
image: javiersantos/android-ci:27.0.0
Build Tools: 27.0.0
Platform: Android 25, 26 & 27
javiersantos/android-ci:26.0.3
image: javiersantos/android-ci:26.0.3
Build Tools: 26.0.3
Platform: Android 25, 26 & 27
javiersantos/android-ci:26.0.2
image: javiersantos/android-ci:26.0.2
Build Tools: 26.0.2
Platform: Android 25, 26 & 27
Sample usages
GitLab
.gitlab-ci.yml

image: javiersantos/android-ci:27.0.3

before_script:
    - export GRADLE_USER_HOME=`pwd`/.gradle
    - chmod +x ./gradlew

cache:
  key: "$CI_COMMIT_REF_NAME"
  paths:
     - .gradle/

stages:
  - build

build:
  stage: build
  script:
     - ./gradlew assembleDebug
  artifacts:
    paths:
      - app/build/outputs/apk/
Bitbucket
bitbucket-pipeline.yml

image: javiersantos/android-ci:27.0.3

pipelines:
  default:
    - step:
        script:
          - export GRADLE_USER_HOME=`pwd`/.gradle
          - chmod +x ./gradlew
          - ./gradlew assembleDebug