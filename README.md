# Typescript-Action-Create-Includes

- [Typescript-Action-Create-Includes](#typescript-action-create-includes)
  - [Inputs](#inputs)
  - [Examples](#examples)
  - [Example usage](#example-usage)

The github action that creates include code files for your project, the changes still need to be submitted afterwards.

Its creates a list of each typescript file in the folder and for each sub folder that has an `include.ts`.

## Inputs

**folder**:
The folder path to start at, use `${{github.workspace}}/source`

## Examples

![example](https://raw.githubusercontent.com/DaanV2/Typescript-Action-Create-Includes/main/assets/example.PNG)

## Example usage

```yml
# This is a basic workflow to help you get started with Actions

name: Create markdown indexes

# Controls when the action will run. 
on:
  # Triggers the workflow on push or pull request events but only for the master branch
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - uses: actions/checkout@v2.3.4

      # Runs a single command using the runners shell
      - uses: DaanV2/Typescript-Action-Create-Includes@v1.0
        with: 
          folder: ${{github.workspace}}

      - name: Commit changes
        continue-on-error: true
        run: |
          cd $GITHUB_WORKSPACE
          git config user.name bot
          git config user.email bot@example.com
          git add .
          git commit -m "auto: Generated markdown indexes pages"
          git push
```
