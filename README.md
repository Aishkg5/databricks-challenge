### STEPS
1. Create Resource group
    1. Create storage account and enable hierarchy 
         1. Create containers
              1. Drivefiles
                 - Upload all dlm files into this container
              2. Oltpraw
                 - ADF will load data 
              3. gsynergymetastore(databricks)
                 - DLT will load data
    2. create data factory
       - Go to adls IAM and give Storage data blob contributor role for adf managed identity
       - Copy code from git
       - Pipeline parameters
           * p_pl_container – drivefiles
           * p_pl_inp_file – no value(for getmetadata)
           * p_pl_dest_container - oltpraw
    3. Create databricks access connector
       - Go to adls IAM and give Storage data blob contributor role for access connector
    4. create databricks workspace
       - go to account console
           1. create metastore
              - container -> gsynergymetastore
              - access connector id
          2.	assign the workspace to the metastore
        - go to workspace
          1.	create catalog gsynergy
          2.	create storage credential
                - using access connector id
          3.	create external location
                - using abfss://oltpraw@{account}.dfs.core.windows.net/
                - using storage credential created above
          4.	create notebook
                - copy the code from git
          5.	attach the notebook to dlt
                - parameters 
                    * Container
                    * StorageAccount
                - Catalog -> gsynergy
                - Schema -> default


**NOTE** - Used online tool to create ER diagram https://erd.dbdesigner.net/
         and Canva for data flow diagram
