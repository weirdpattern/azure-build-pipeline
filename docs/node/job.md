# Node
Installs `node.js` in the virtual machine defined by `vmImage` and execute all 
provided `steps`.


## Parameters
The job accepts two kinds of parameters:


### Pipeline scope
The reason for these parameters is to allow overriding the pipeline variables
via the azure-pipeline.yml file of the specific project.  

- `debug` 
  Scope: Optional  
  Defaults: Value from `pipeline.debug`  
  Description: Enables debug information in the job.

- `build_tool` 
  Scope: Required  
  Defaults: Value from `pipeline.build_tool`  
  Description: Defines the build tool to be used in the job.  
  Possible values: yarn, npm.


### Job scope

- `name` 
  Scope: Required  
  Defaults: linux  
  Description: Defines the name of the job.

- `vmImage` 
  Scope: Required  
  Defaults: ubuntu-16.04  
  Description: Defines the virtual machine image to be used to run the job.

- `matrix` 
  Scope: Required  
  Defaults: latest available version  
  Description: Defines the node version to be installed.  
  Requires to be updated when a new version of node is available.  

- `steps` 
  Scope: Required  
  Defaults: Empty array  
  Description: Defines the steps to be executed by the job.


## Variables
The job generates two different variables that are passed to all steps as 
parameters giving the developer the option to override these values in each step.  

- `debug`
  Calculated from the parameter `debug` and the system variable `system.debug`.  
  If any of these is true, the debug variable will be true and all steps will use it.  

  i.e. `or (parameters.debug, variables.system.debug)`

- `build_tool`
  Calculates from the parameter `build_tool`.
  