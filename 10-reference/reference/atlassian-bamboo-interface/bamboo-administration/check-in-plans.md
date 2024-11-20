# Check-In Plans

MettleCI's Check-In Plans page is for linking DataStage project with a Check-in plan on the bamboo server. Every time user [https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/292356154](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/292356154), bamboo will automatically run the specified plan with provided parameters to commit the changes.

> [!INFO]
> This administration page is available after installing the **MettleCI - Git Plugin** (dm-git-plugin<version>.jar)

## To add new Check-in Plan

Steps

1.  Navigate to Bamboo Administration page.
2.  Click on Check-in Plans under Mettle section on the left panel.
3.  Click **Add Checkin Plan** button and fill in the values
    
    |     |     |
    | --- | --- |
    | DataStage Engine | <Datastage Engine Name> |
    | DataStage Project | <Datastage Project Name> |
    | Bamboo Plan | <Bamboo Plan> <br><br>Select check-in plan that you have setup |
    
    ![](./attachments/image2018-5-23_17-3-15.png)
    
4.  Click **Create**