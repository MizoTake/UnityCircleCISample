# 「unity-ci」 CircleCI Orb for Unity

[![CircleCI](https://circleci.com/gh/MizoTake/unity-ci.svg?style=svg)](https://circleci.com/gh/MizoTake/unity-ci)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
[![Actions Status](https://github.com/MizoTake/unity-ci/workflows/unity-ci-example/badge.svg)](https://github.com/MizoTake/unity-ci/actions)

unity-ci orbの公式ページ

[mizotake/unity-ci](https://circleci.com/orbs/registry/orb/mizotake/unity-ci)

## Example config.yml

```yaml:config.yml
version: 2.1

orbs:
  unity-ci: mizotake/unity-ci@0.0.9

executors:
  unity_executor:
    docker:
      - image: gableroux/unity3d:2019.1.0f2

workflows:
  version: 2
  unity-ci-test:
    jobs:
      - unity-ci/build:
          name: Build Execute Win
          exec: unity_executor
          platform: Win
          method: Build.Method
          zip: true
      - unity-ci/build:
          name: Build Execute WebGL
          exec: unity_executor
          platform: WebGL
          method: Build.Method
          zip: true
      - unity-ci/build:
          name: Build Execute OSXUniversal
          exec: unity_executor
          platform: OSXUniversal
          method: Build.Method
          zip: true
      - unity-ci/test:
          name: Edit Mode Test
          exec: unity_executor
          mode: editmode
      - unity-ci/test:
          name: Play Mode Test
          exec: unity_executor
          mode: playmode
      - unity-ci/execute_method:
          name: Exeucte Method
          exec: unity_executor
          method: Execute.Method

```

## commands

### unity_activate

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|license|Unity License|-|UNITY_LICENSE_BASE64|env_var_name|

### build

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|platform|Build Target Platform|:white_check_mark:|-|string|
|method|Build Execute Method|:white_check_mark:|-|string|
|no_output_timeout|No Output Timeout|-|10m|string|

### test

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|mode|Test Target Platform|:white_check_mark:|-|string|

### execute_method

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|method|Target Method|:white_check_mark:|-|string|

### zip

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|directory|Target Directory|:white_check_mark:|-|string

## jobs

### build

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|exec|-|:white_check_mark:|-|executor|
|license|Unity License|-|UNITY_LICENSE_BASE64|env_var_name
method|Build Execute Method|:white_check_mark:|-|string
platform|Test Target Platform|:white_check_mark:|-|string
zip|Archive Build Contents|-|false|boolean
no_output_timeout|No Output Timeout|-|10m|string
directory|Target Directory|-|.|string|

### test

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|exec|-|:white_check_mark:|-|executor|
|license|Unity License|-|UNITY_LICENSE_BASE64|env_var_name
|mode|Test Target Mode|:white_check_mark:|-|string|

### execute_method

|PARAMETER|DESCRIPTION|REQUIRED|DEFAULT|TYPE|
|---|---|---|---|---|
|exec|-|:white_check_mark:|-|executor|
|license|Unity License|-|UNITY_LICENSE_BASE64|env_var_name
|method|Build Execute Method|:white_check_mark:|-|string|
