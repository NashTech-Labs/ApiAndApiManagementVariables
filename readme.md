# ApiAndApiManagementVariables.setVariables

## Pipeline Requirements

The setVariable pipeline requires the following parameters to be defined:
Paramaters:


| Name  | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| appDeploymentTarget | string | | | Required | |
| key | string | | | Required | |
| apiAppServiceNames | string | | | Optional | |
| apiArchivePattern | string | | | Optional | |
| apiExtractFolder | string | | | Optional | |
| apiPackageId | string | | | Optional | |
| apiPacakgeVersion | string | | | Optional | |
| apiImage | string | | | Optional | |
| apiAKSApps | string | | | Optional | |
| apiAKSAppsForBlueGreen | string | | | Optional | |
| apiWorkloadName | string | | | Optional | |
| apimInstanceNames | string | | | Optional | |
| apiSpecificationArchivePattern | string | | | Optional | |
| apiSpecificationExtractFolder | string | | | Optional | |
| apiSpecificationAPIId | string | | | Optional | |
| apiPath | string | | | Optional | |
| apiSpecificationName | string | | | Optional | |
| apiSpecificationDescription | string | | | Optional | |
| apiSpecificationPackageId | string | | | Optional | |
| apiSpecificationPacakgeVersion | string | | | Optional | |
| enableApiAndApiManagementVariables | boolean | 'true' | 'true'/'false' | Required | |

These parameters provide multiple use case options for the setvariables templates pipeline, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

### Direct use of a template

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/terraform.validate.ado
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'



  steps:
  # passing the parameters
  - template: templates/SetApiAndApiManagementVariables.yml
        parameters:
          appDeploymentTarget: ${{parameters.appDeploymentTarget}}
          key: ${{parameters.key}}
          apiAKSApps: ${{ parameters.apiAKSApps}}
          apiAKSAppsForBlueGreen: ${{ parameters.apiAKSAppsForBlueGreen}}
          apiWorkloadName: ${{ parameters.apiWorkloadName}}
          apiAppServiceNames: ${{ parameters.apiAppServiceNames}}
          apiArchivePattern: ${{ parameters.apiArchivePattern}}
          apiExtractFolder: ${{ parameters.apiExtractFolder}}
          apiPackageId: ${{ parameters.apiPackageId}}
          apiPacakgeVersion: ${{ parameters.apiPacakgeVersion}}
          apiImage: ${{ parameters.apiImage}}
          apimInstanceNames: ${{ parameters.apimInstanceNames}}
          apiPath: ${{ parameters.apiPath}}
          apiSpecificationAPIId: ${{ parameters.apiSpecificationAPIId}}
          apiSpecificationArchivePattern: ${{ parameters.apiSpecificationArchivePattern}}
          apiSpecificationExtractFolder: ${{ parameters.apiSpecificationExtractFolder}}
          apiSpecificationName: ${{ parameters.pipelineName}}
          apiSpecificationDescription: ${{ parameters.apiSpecificationDescription}}
          apiSpecificationPackageId: ${{ parameters.apiSpecificationPackageId}}
          apiSpecificationPacakgeVersion: ${{ parameters.apiSpecificationPacakgeVersion}}

  # passing the variables as parameters
  - template: templates/SetApiAndApiManagementVariables.yml@Template
      parameters:
        appDeploymentTarget: ${{parameters.appDeploymentTarget}}
        key: ${{parameters.key}}
        apiAKSApps: refdata-$(platform.refdata.blueGreenEnv)
        apiAKSAppsForBlueGreen: refdata-{deploymentSlot}
        apiWorkloadName: refdata
        apiAppServiceNames: $(platform.refdata.webAppName)
        apiArchivePattern: refdata-website.$(build.configVersion).*
        apiExtractFolder: $(build.configVersion)/refdata-website
        apiPackageId: refdata-website
        apiPacakgeVersion: $(build.configVersion)
        apiImage: refdata:v$(build.configVersion)
        apimInstanceNames: $(environment.apiManagement.serviceNames)
        apiPath: refdata
        apiSpecificationAPIId: $(platform.refdata.apiManagement.name)
        apiSpecificationArchivePattern: refdata-apispecification.$(build.configVersion).*
        apiSpecificationExtractFolder: $(build.configVersion)/refdata-apispecification
        apiSpecificationName: 'RefData API'
        apiSpecificationDescription: 'API for RefData operations.'
        apiSpecificationPackageId: refdata-apispecification
        apiSpecificationPacakgeVersion: $(build.configVersion)
        
  
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```

