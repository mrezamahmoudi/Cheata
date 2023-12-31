# Chart Management

#### Creates a chart directory along with the common files and directories used in a chart.

> helm create <name>
#### Packages a chart into a versioned chart archive file.

> helm package <chart-path>
#### Run tests to examine a chart and identify possible issues:

> helm lint <chart>
#### Inspect a chart and list its contents:

> helm show all <chart>
#### Displays the contents of the values.yaml file

> helm show values <chart>
#### Download/pull chart

> helm pull <chart>
#### If set to true, will untar the chart after downloading it

> helm pull <chart> --untar=true
#### Verify the package before using it

> helm pull <chart> --verify
#### Default-latest is used, specify a version constraint for the chart version to use

> helm pull <chart> --version <number>
#### Display a list of a chart’s dependencies:

> helm dependency list <chart>



# Install and Uninstall Apps

#### Install the chart with a name

> helm install <name> <chart>                           
#### Install the chart in a specific namespace

> helm install <name> <chart> --namespace <namespace>   
#### Set values on the command line (can specify multiple or separate values with commas)

> helm install <name> <chart> --set key1=val1,key2=val2 
#### Install the chart with your specified values

> helm install <name> <chart> --values <yaml-file/url>  
#### Run a test installation to validate chart (p)

> helm install <name> <chart> --dry-run --debug         
#### Verify the package before using it

> helm install <name> <chart> --verify                  
#### update dependencies if they are missing before installing the chart

> helm install <name> <chart> --dependency-update       
#### Uninstall a release

> helm uninstall <name>                                 

# Perform App Upgrade and Rollback

#### Upgrade a release

> helm upgrade <release> <chart>                            
#### If set, upgrade process rolls back changes made in case of failed upgrade.

> helm upgrade <release> <chart> --atomic                   
#### update dependencies if they are missing before installing the chart

> helm upgrade <release> <chart> --dependency-update        
#### specify a version constraint for the chart version to use

> helm upgrade <release> <chart> --version <version_number> 
#### specify values in a YAML file or a URL (can specify multiple)

> helm upgrade <release> <chart> --values                   
#### Set values on the command line (can specify multiple or separate valuese)

> helm upgrade <release> <chart> --set key1=val1,key2=val2  
#### Force resource updates through a replacement strategy

> helm upgrade <release> <chart> --force                    
#### Roll back a release to a specific revision

> helm rollback <release> <revision>                        
#### Allow deletion of new resources created in this rollback when rollback fails

> helm rollback <release> <revision>  --cleanup-on-fail     

# List, Add, Remove, and Update Repositories

#### Add a repository from the internet:

> helm repo add <repo-name> <url>   
#### List added chart repositories

> helm repo list                    
#### Update information of available charts locally from chart repositories

> helm repo update                  
#### Remove one or more chart repositories

> helm repo remove <repo_name>      
#### Read the current directory and generate an index file based on the charts found.

> helm repo index <DIR>             
#### Merge the generated index with an existing index file

> helm repo index <DIR> --merge     
#### Search repositories for a keyword in charts

> helm search repo <keyword>        
#### Search for charts in the Artifact Hub or your own hub instance

> helm search hub <keyword>         

# Helm Release monitoring

#### Lists all of the releases for a specified namespace, uses current namespace context if namespace not specified

> helm list                                   
#### Show all releases without any filter applied, can use -a

> helm list --all                             
#### List releases across all namespaces, we can use -A

> helm list --all-namespaces                  
#### Selector (label query) to filter on, supports '=', '==', and '!='

> helm -l key1=value1,key2=value2             
#### Sort by release date

> helm list --date                            
#### Show deployed releases. If no other is specified, this will be automatically enabled

> helm list --deployed                        
#### Show pending releases

> helm list --pending                         
#### Show failed releases

> helm list --failed                          
#### Show uninstalled releases (if 'helm uninstall --keep-history' was used)

> helm list --uninstalled                     
#### Show superseded releases

> helm list --superseded                      
#### Prints the output in the specified format. Allowed values: table, json, yaml (default table)

> helm list -o yaml                           
#### This command shows the status of a named release.

> helm status <release>                       
#### if set, display the status of the named release with revision

> helm status <release> --revision <number>   
#### Historical revisions for a given release.

> helm history <release>                      
#### Env prints out all the environment information in use by Helm.

> helm env                                    

# Download Release Information

#### A human readable collection of information about the notes, hooks, supplied values, and generated manifest file of the given release.

> helm get all <release>     
#### This command downloads hooks for a given release. Hooks are formatted in YAML and separated by the YAML '---\n' separator.

> helm get hooks <release>   
#### A manifest is a YAML-encoded representation of the Kubernetes resources that were generated from this release's chart(s). If a chart is dependent on other charts, those resources will also be included in the manifest.

> helm get manifest <release> 
#### Shows notes provided by the chart of a named release.

> helm get notes <release>   
#### Downloads a values file for a given release. use -o to format output

> helm get values <release>  

# Plugin Management

#### Install plugins

>helm plugin install <path/url1>     
#### View a list of all installed plugins

>helm plugin list                    
#### Update plugins

>helm plugin update <plugin>         
#### Uninstall a plugin

>helm plugin uninstall <plugin>      
