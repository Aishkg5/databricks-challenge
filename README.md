1.	Create Resource group
  a.	Create storage account and enable hierarchy 
    i.	Create containers
        1.	Drivefiles
            a.	Upload all dlm files into this container
        2.	Oltpraw
            a.	ADF will load data 
        3.	gsynergymetastore(databricks)
            a.	DLT will load data
  b.	create data factory
    i.	Go to adls IAM and give Storage data blob contributor role for adf managed identity
    ii.	Copy code from git
    iii.	Pipeline parameters
          1.	p_pl_container – derivefiles
          2.	p_pl_inp_file – no value(for getmetadata)
          3.	p_pl_dest_container - oltpraw
  c.	Create databricks access connector
      i.	Go to adls IAM and give Storage data blob contributor role for access connector
  d.	create databricks workspace
      i.	go to account console
          1.	create metastore
              a.	container- gsynergymetastore
              b.	access connector id
          2.	assign the workspace to the metastore
      ii.	go to workspace
          1.	create catalog gsynergy
          2.	create storage credential
              a.	using access connector id
          3.	create external location
              a.	using abfss://oltpraw@{account}.dfs.core.windows.net/
              b.	using storage credential created above
          4.	create notebook
              a.	copy the code from git
          5.	attach the notebook to dlt
              a.	parameters 
                  i.	Container
                  ii.	StorageAccount
              b.	Catalog - gsynergy
              c.	Schema -default
