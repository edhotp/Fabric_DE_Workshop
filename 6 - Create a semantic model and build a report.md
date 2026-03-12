# Lakehouse tutorial: Create a semantic model and build a report

In this section of the tutorial, you create a semantic model from your lakehouse data and define the relationships between fact and dimension tables. With the data model in place, you can build Power BI reports.

## Prerequisites

Before you begin, you must complete the previous tutorials in this series:

1. [Create a workspace](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-get-started)
2. [Create a lakehouse](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-build-lakehouse)
3. [Ingest data into the lakehouse](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-data-ingestion)
4. [Prepare and transform the data](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-data-preparation)

## Create a semantic model

Power BI is natively integrated in Fabric. When you create a semantic model from a lakehouse, it uses [Direct Lake](https://learn.microsoft.com/en-us/fabric/fundamentals/direct-lake-overview) mode, which loads data directly from OneLake into memory for fast analysis without importing or duplicating data.

1. In your browser, go to your Fabric workspace in the [Fabric portal](https://app.fabric.microsoft.com/).
2. Select the **wwilakehouse** lakehouse to open it.
3. Select **SQL analytics endpoint** from the **Lakehouse** dropdown menu at the top right of the screen.

    [![Screenshot showing where to find and select SQL analytics endpoint from the top right dropdown menu.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/load-data-choose-sql-endpoint.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/load-data-choose-sql-endpoint.png#lightbox)

    From the SQL analytics endpoint pane, you should be able to see all the tables you created. If you don't see them yet, select the **Refresh** icon at the top left.

4. Select **New semantic model** from the ribbon.
5. In the **New semantic model** dialog box:

    - Enter a name for your semantic model (for example, "WWI Sales Model")
    - Select the workspace to save it in
    - Select all the tables you created in this tutorial series
    - Select **Confirm**

### Troubleshoot missing tables with lakehouse schemas

If you enabled [lakehouse schemas](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-schemas) and get an error like "We can't access the source Delta table" when creating the semantic model, the tables might not be registered in the Spark metastore. To resolve the issue, open a notebook attached to your lakehouse and run the following code to explicitly register the tables:

> [!TIP]
> You can go back to the notebook you used in the [previous tutorial](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-data-preparation) and add this code as a new cell instead of creating a new notebook.

```python
tables = ['fact_sale', 'dimension_city', 'dimension_customer', 'dimension_date',
          'dimension_employee', 'dimension_stock_item',
          'aggregate_sale_by_date_city', 'aggregate_sale_by_date_employee']

for table in tables:
    df = spark.read.format("delta").load(f"Tables/{table}")
    df.write.mode("overwrite").option("overwriteSchema", "true").format("delta").saveAsTable(table)
```

After the code runs successfully, go back to the SQL analytics endpoint and create the semantic model again.

## Define table relationships

To create reports that combine data from multiple tables, you define relationships between the fact table and each dimension table. These relationships tell Power BI how to join the tables when building visualizations.

1. Go to your workspace and select the semantic model you created to open it.
2. Select **Open** from the toolbar to open the web modeling experience.
3. In the top right corner, select the dropdown and choose **Editing** to switch to editing mode.
4. From the **fact_sale** table, select and drag the **CityKey** field to the **CityKey** field in the **dimension_city** table to create a relationship.

    [![Screenshot showing drag and drop fields across tables to create relationships.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/drag-drop-tables-relationships.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/drag-drop-tables-relationships.png#lightbox)

5. The **New relationship** dialog box appears with the following default settings:

    - **From table**: **fact_sale** and the column **CityKey**.
    - **To table**: **dimension_city** and the column **CityKey**.
    - **Cardinality**: **Many to one (*:1)**.
    - **Cross filter direction**: **Single**.
    - **Make this relationship active**: selected.

    Select the box next to **Assume referential integrity**, and then select **Save**.

    [![Screenshot of the New relationship dialog box, showing where to select Assume referential integrity.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/create-relationship-dialog.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/create-relationship-dialog.png#lightbox)

    > [!NOTE]
    > When defining relationships for this report, make sure **fact_sale** is always the **From table** and the **dimension_\*** table is the **To table**, not vice versa.

6. Repeat the previous steps to create relationships for the remaining dimension tables. For each relationship, select and drag the key column from **fact_sale** to the matching column in the dimension table. Use the same **New relationship** settings as before, including **Assume referential integrity**.

    | **Drag from fact_sale** | **To table** | **To column** |
    | --- | --- | --- |
    | StockItemKey | dimension_stock_item | StockItemKey |
    | SalespersonKey | dimension_employee | EmployeeKey |
    | CustomerKey | dimension_customer | CustomerKey |
    | InvoiceDateKey | dimension_date | Date |

    After you add these relationships, your data model is ready for reporting as shown in the following image:

    [![Screenshot of a New report screen showing multiple table relationships.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/new-report-relationships.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-build-report/new-report-relationships.png#lightbox)

## Build a report

With the semantic model and relationships in place, your data model is ready for reporting. From the semantic model, select **New report** in the ribbon to open the Power BI report canvas where you can create visualizations using your data.

To learn more about creating reports, see [Create reports on semantic models in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/create-reports).

## Next step

> [Clean up resources](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-clean-up)
