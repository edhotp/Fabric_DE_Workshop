# Lakehouse tutorial: Ingest data into the lakehouse

In this tutorial, you ingest more dimensional and [fact tables](https://learn.microsoft.com/en-us/fabric/data-warehouse/dimensional-modeling-fact-tables) from the Wide World Importers (WWI) into the lakehouse. Pipelines enable you to ingest data at scale with the option to schedule data workflows.

## Prerequisites

- If you don't have a lakehouse, you must [create a lakehouse](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-build-lakehouse).

## Ingest data

In this section, you use the **Copy data activity** of the Data Factory pipeline to ingest sample data from an Azure storage account to the **Files** section of the [lakehouse you created in the previous tutorial](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-build-lakehouse).

1. In the workspace you created in the previous tutorial, select **New item**.
2. Search for **Pipeline** in the search bar and select the **Pipeline** tile.
3. In the **New pipeline** dialog box, specify the name as **IngestDataFromSourceToLakehouse** and select **Create**.
4. From your new pipeline's **Home** tab, select **Pipeline activity** > **Copy data**.

    [![Screenshot showing where to select Pipeline activity and Copy data.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/pipeline-copy-data.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/pipeline-copy-data.png#lightbox)

5. Select the new **Copy data** activity from the canvas. Activity properties appear in a pane below the canvas, organized across tabs including **General**, **Source**, **Destination**, **Mapping**, and **Settings**. You might need to expand the pane upwards by dragging the top edge.
6. On the **General** tab, enter **Data Copy to Lakehouse** in the **Name** field. Leave the other fields with their default values.

    [![Screenshot showing where to add the copy activity name on the General tab.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/data-copy-to-lakehouse.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/data-copy-to-lakehouse.png#lightbox)

7. On the **Source** tab, select the **Connection** dropdown and then select **Browse all**.
8. In the **Choose a data source to get started** page, search for and select **Azure blobs**.
9. Enter the following details in the **Connect data source** page. Then select **Connect** to create the connection to the data source. For this tutorial, all the sample data is available in a public container of Azure blob storage. You connect to this container to copy data from it.

    | Property | Value |
    | --- | --- |
    | Account name or URL | `https://fabrictutorialdata.blob.core.windows.net/sampledata/` |
    | Connection | Create new connection |
    | Connection name | wwisampledata |
    | Authentication kind | Anonymous |

    [![Screenshot showing where to select blob storage connection.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/data-store-source-blob.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/data-store-source-blob.png#lightbox)

10. On the **Source** tab, the newly created connection is selected by default. Specify the following properties before moving to the destination settings.

    | Property | Value |
    | --- | --- |
    | Connection | wwisampledata |
    | File path type | File path |
    | File path | Container name (first text box): sampledata  Directory name (second text box): WideWorldImportersDW/parquet |
    | Recursively | Checked |
    | File format | Binary |

    [![Screenshot showing the Blob Storage connection settings.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/blob-storage-connection-settings.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/blob-storage-connection-settings.png#lightbox)

11. On the **Destination** tab, specify the following properties:

    | Property | Value |
    | --- | --- |
    | Connection | wwilakehouse (choose your lakehouse if you named it differently) |
    | Root folder | Files |
    | File path | Directory name (first text box): wwi-raw-data |
    | File format | Binary |

    [![Screenshot of the destination tab, showing where to enter specific details.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/destination-settings.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/destination-settings.png#lightbox)

12. You have configured the copy data activity. Select the **Save** icon on the top ribbon (below Home) to save your changes, and select **Run** to execute your pipeline and its activity. You can also schedule pipelines to refresh data at defined intervals to meet your business requirements. For this tutorial, we run the pipeline only once by selecting **Run**.
13. This action triggers data copy from the underlying data source to the specified lakehouse and might take up to a minute to complete. You can monitor the execution of the pipeline and its activity under the **Output** tab. The activity status changes from **Queued** > **In progress** > **Succeeded**.

    [![Screenshot showing where to select Save and Run the pipeline.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/save-run-output-tab.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/save-run-output-tab.png#lightbox)

    > [!TIP]
    > Select **View Run details** to see more information about the run.

14. After the copy activity is successful, open your lakehouse (wwilakehouse) to view the data. Refresh the **Files** section to see the ingested data. A new folder **wwi-raw-data** appears in the files section, and data from Azure Blob tables is copied there.

    [![Screenshot showing blob data copied into destination lakehouse.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/validate-data-lakehouse.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-data-ingestion/validate-data-lakehouse.png#lightbox)

To load incremental data into a lakehouse, see [Incrementally load data from a data warehouse to a lakehouse](https://learn.microsoft.com/en-us/fabric/data-factory/tutorial-incremental-copy-data-warehouse-lakehouse).

## Next step

> [Prepare and transform data](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-data-preparation)
