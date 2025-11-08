IMPORTANT ❗ ❗ ❗ Please remember to destroy all the resources after each work session. You can recreate infrastructure by creating new PR and merging it to master.
  
![img.png](doc/figures/destroy.png)

1. Authors:

   ***Grupa z10***

   ***https://github.com/mbartn/tbd-workshop-1***
   
2. Follow all steps in README.md.

3. From avaialble Github Actions select and run destroy on main branch.
   
4. Create new git branch and:
    1. Modify tasks-phase1.md file.
    
    2. Create PR from this branch to **YOUR** master and merge it to make new release. 

    3. ![img.png](img.png)

5. Analyze terraform code. Play with terraform plan, terraform graph to investigate different modules.

    ![graph.png](modules/metastore/graph.png)
 
    ***Metastore***
   
    Metastore module deploys the Dataproc Metastore - a fully managed Apache Hive Metastore. 
    It can be used to manage data lake metadata and to provide interoperability between the various data processing 
    engines and tools that are in use.

    The module exposes 4 input variables - `project_name`, `region`, `network` and `metastore_version`. 
    
    Two resources are being created: 
    - `google_project_service` - enables Google Cloud metastore API
    - `google_dataproc_metastore_service` - deploys the actual service. 
    
   
6. Reach YARN UI
   
    ```bash
    gcloud compute ssh tbd-cluster-m --zone "europe-west1-d" --tunnel-through-iap --project "tbd-2025z-342188" -- -L 8088:localhost:8088
    ```
   ![img_1.png](img_1.png)
   
7. Draw an architecture diagram (e.g. in draw.io) that includes:
    1. Description of the components of service accounts
    2. List of buckets for disposal
    
    ***place your diagram here***

8. Create a new PR and add costs by entering the expected consumption into Infracost
For all the resources of type: `google_artifact_registry`, `google_storage_bucket`, `google_service_networking_connection`
create a sample usage profiles and add it to the Infracost task in CI/CD pipeline. Usage file [example](https://github.com/infracost/infracost/blob/master/infracost-usage-example.yml) 

   ***place the expected consumption you entered here***

   ***place the screenshot from infracost output here***

9. Create a BigQuery dataset and an external table using SQL
    
    ***place the code and output here***
   
    ***why does ORC not require a table schema?***

10. Find and correct the error in spark-job.py

    ***describe the cause and how to find the error***

11. Add support for preemptible/spot instances in a Dataproc cluster

    ***place the link to the modified file and inserted terraform code***
    
12. Triggered Terraform Destroy on Schedule or After PR Merge. Goal: make sure we never forget to clean up resources and burn money.

Add a new GitHub Actions workflow that:
  1. runs terraform destroy -auto-approve
  2. triggers automatically:
   
   a) on a fixed schedule (e.g. every day at 20:00 UTC)
   
   b) when a PR is merged to main containing [CLEANUP] tag in title

Steps:
  1. Create file .github/workflows/auto-destroy.yml
  2. Configure it to authenticate and destroy Terraform resources
  3. Test the trigger (schedule or cleanup-tagged PR)
     
***paste workflow YAML here***

***paste screenshot/log snippet confirming the auto-destroy ran***

***write one sentence why scheduling cleanup helps in this workshop***
