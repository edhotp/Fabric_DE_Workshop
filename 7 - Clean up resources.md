# Lakehouse tutorial: Clean up Fabric resources

In this tutorial, you delete the resources you created in the previous tutorials to avoid unnecessary consumption of capacity. You can delete individual items or remove the entire workspace.

## Delete individual items

To clean up specific items without removing the entire workspace, go to your workspace and delete the items you no longer need.

1. Select your workspace from the navigation menu to open the workspace item view.
2. Select the **...** (ellipsis) menu next to the item you want to delete, and then select **Delete**.

You can delete any of the items you created in this tutorial, including:

- The **wwilakehouse** lakehouse (and its associated SQL analytics endpoint)
- The semantic model you created for reporting
- Any notebooks you used for data preparation and transformation
- The data pipeline you created for data ingestion

## Delete the workspace

If you created a workspace specifically for this tutorial, you can delete the entire workspace and all its contents at once.

1. Select your workspace from the navigation menu to open the workspace item view.

    [![Screenshot of the left navigation menu, showing where to select your workspace.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-clean-up/select-workspace-item.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-clean-up/select-workspace-item.png#lightbox)

2. Select **Workspace settings**.

    [![Screenshot of the workspace item view, showing where to select Workspace settings.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-clean-up/select-workspace-settings.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-clean-up/select-workspace-settings.png#lightbox)

3. Select **Other** and **Remove this workspace**.

    [![Screenshot of the Workspace settings pane, showing where to select Other and Remove this workspace.](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-clean-up/remove-this-workspace.png)](https://learn.microsoft.com/en-us/fabric/data-engineering/media/tutorial-lakehouse-clean-up/remove-this-workspace.png#lightbox)

4. When the warning appears, select **Delete**.

## Related content

- [Options to get data into the Fabric Lakehouse](https://learn.microsoft.com/en-us/fabric/data-engineering/load-data-lakehouse)
