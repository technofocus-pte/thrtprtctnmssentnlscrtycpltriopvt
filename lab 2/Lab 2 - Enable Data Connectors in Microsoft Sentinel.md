# Lab 2 - Enable Data Connectors in Microsoft Sentinel

## Objectives

In this Lab you will learn how to enable Data Connectors in Microsoft
Sentinel to bring alerts and/or telemetry from different sources.

**Prerequisites**

This lab assumes that you have completed **Lab 1**, as you will need an
Microsoft Sentinel workspace provisioned.

**Some of the data connectors that will be used in this lab, require
some specific permissions on the workspace or your azure subscription.
If you don't have the appropriate permissions, you can still continue
doing the rest of the labs.**

## Exercise 1 - Enabling Data Connectors in Microsoft Sentinel

### Task 1: Enable and Install the Data connectors.

This exercise shows you how to enable Data connectors.

1.  On the Azure Portal https://portal.azure.com and search
    for Microsoft Sentinel and click on **Microsoft Sentinel**.

![](./media/image1.png)

2.  Select **SentWrkspcXXXXXX**.

![](./media/image2.png)

3.  Now select **Data Connectors** under **Configuration** section.

![](./media/image3.png)

4.  You should get the message **Data Connector with "content source =
    gallery content" have been removed.** In that message select
    the **Click here** link

![](./media/image4.png)

5.  On the **Out-of-the-box Content Centralization** page click
    on **Continue**

![](./media/image5.png)

6.  Click on the **Complete centralization** button

![](./media/image6.png)

7.  You should receive the notification as shown in below image

![](./media/image7.png)

**Note** - Sometime it may not install any connector, which is also fine
to proceed ahead with the Labs.

8.  From the top click on the link for **Microsoft Sentinel** or
    navigate back to the Sentinel page.

![](./media/image8.png)

9.  Click on the **Refresh** button and you should be able to see the
    few connectors Data connectors showing.

![](./media/image9.png)

**Note** - Sometime it may not install any connector, which is also fine
to proceed ahead with the Labs.

10. Click on **Content hub** under **Content management**

![](./media/image10.png)

11. On the Content hub page search for Azure Activity and then
    select **Azure Activity** content and click on **Install** button

![](./media/image11.png)

12. On the Content hub page search for Microsoft defender for cloud and
    then select **Microsoft Defender for Cloud** content and click
    on **Install** button

![](./media/image12.png)

13. On the Content hub page search for Threat Intelligence and then
    select **Microsoft Defender Threat Intelligence (preview)** content
    and click on **Install** button

![](./media/image13.png)

### Task 2 - Enabling Azure Activity data connector

This exercise shows you how to enable Data connectors.

1.  On the **Azure Portal** http://portal.azure.com search for Microsoft
    Sentinel and click on **Microsoft Sentinel**.

![A screenshot of a computer Description automatically
generated](./media/image14.png)

2.  Select **SwrkXXXXXXX**.

![A screenshot of a computer Description automatically
generated](./media/image15.png)

3.  Now select **Data Connectors** under **Configuration** section.

![](./media/image16.png)

4.  You should be able to see the **Data connectors** already available
    based on the selection made during the deployment.

![](./media/image17.png)

5.  On the data connectors screen, select the **Azure
    Activity** connector and click on **Open connector page**.

![](./media/image18.png)

6.  On the **Azure Activity connector** page, go to option number **2.
    Connect your subscriptions through diagnostic settings new
    pipeline**. This method leverages Azure Policy and it brings many
    improvements compared to the old method (more details about these
    improvements can be found here). Click on the **Launch Azure Policy
    Assignment** wizard, this will redirect you to the policy creation
    page.

![A screenshot of a computer Description automatically
generated](./media/image19.png)

7.  On the **Scope** selection select **Azure Pass - Sponsorship** . do
    not select any Click **Select**.

![](./media/image20.png)

8.  Go to the **Parameters** tab. On the **Primary Log Analytics
    workspace** select the **SwrkXXXXXXX**.

![](./media/image21.png)

9.  Under **Remediation** tab, select the check box besides **Create a
    remediation task** and then click on **Review + create** button

![A screenshot of a computer Description automatically
generated](./media/image22.png)

10. On the **Review + create** tab, click on the **Create** button.

![A screenshot of a computer Description automatically
generated](./media/image23.png)

11. In the **Notification** pane you will be able to see the '**Role
    Assignments creation succeeded**', '**Remediation task creation
    succeeded**' and '**Creating policy assignment succeeded**'
    notifications.

![A screenshot of a computer Description automatically
generated](./media/image24.png)

12. On the **Azure Activity connector** page you will be able to see the
    connection status.

**Note**: It is normal if you don't immediately see the connector
showing as connected and in green, it takes **around 30 minutes** for
the process to complete. Also, each subscription has a maximum of 5
destinations for its activity logs. If this limit is already reached,
the policy created as part of this exercise won't be able to add an
additional destination to your Microsoft Sentinel workspace.

![A screenshot of a computer Description automatically
generated](./media/image25.png)

13. Continue to the next task then you can check back after 30 minutes.

14. Close the **Azure Activity** connector blade to go back to
    the **Data Connectors** page.

### Task 3 - Enabling Microsoft Defender for Cloud data connectors

This task shows you how to enable the Microsoft Defender for Cloud data
connectors. This connector allows you to stream your security alerts
from Microsoft Defender for Cloud into Microsoft Sentinel, so you can
view Defender data in workbooks, query it to produce alerts, and
investigate and respond to incidents.

1.  While still on the **Microsoft Sentinel** page click on **Data
    Connectors** under **Configuration** section.

![](./media/image26.png)

2.  In the **Data connectors** screen, type tenant in the search bar,
    select the **Tenant-based Microsoft Defender for
    Cloud** **(Preview)** connector and click on **Open connector
    page**.

![](./media/image27.png)

![](./media/image28.png)

**Note** - If you receive the error **Data Connector Not Found**, then
navigate to **Content Hub** and then Reinstall the **Microsoft Defender
for Cloud Connector** again, close the browser and relaunch it. Navigate
to the Azure Portal https://portal.azure.com

![](./media/image29.png)

3.  On the **Tenant-based Microsoft Defender for
    Cloud** **(Preview)** connector page,
    under **Configuration** section click on the **Connect** button.

![](./media/image30.png)

4.  You should receive the notification as **Connected successfully.**

![](./media/image31.png)

5.  Wait for 1-2 minutes and then refresh the page, the Status of the
    connector should also be updated to **Connected.**

![](./media/image32.png)

6.  Back on the **Data connectors** screen, type subscription in the
    search bar, select the **Subscription-based Microsoft Defender for
    Cloud** **(legacy)** connector and click on **Open connector page**.

![](./media/image33.png)

7.  On the **Subscription-based Microsoft Defender for
    Cloud** **(legacy)** connector page,
    under **Configuration** section, select the **Azure Pass –
    Sponsorship** subscription and then click on the **Connect** button.

![](./media/image34.png)

8.  You should receive the notification as **Connected successfully**.

![](./media/image35.png)

9.  The Status of the connector should also be updated to **Connected.**

![](./media/image36.png)

### Task 4 - Enabling Microsoft Defender Threat Intelligence connector

The **Microsoft Defender Threat Intelligence** (MDTI) connector to your
Sentinel workspace, which ingests Microsoft Threat Intelligence
indicators automatically into the ThreatIntelligenceIndicator table.
MDTI provides a set of indicators and access to
the https://ti.defender.microsoft.com portal at no additional cost, with
the premium features of the MDTI portal and API requiring licensing.

The *Threat Intelligence* content solution includes the data connectors
for all supported forms of Threat Intelligence.

**NOTE:** Sentinel also supports importing Threat Intelligence
indicators via the TAXII protocol using the **Threat Intelligence -
TAXII** data connector, so if you have your own preferred TI source, you
can add that to your workspace instead.

1.  On the **Azure Portal** http://portal.azure.com search for Microsoft
    Sentinel and click on **Microsoft Sentinel**.

![A screenshot of a computer service Description automatically
generated](./media/image37.png)

2.  Select **SwrkXXXXXXX**.

![A screenshot of a computer Description automatically
generated](./media/image38.png)

3.  From the left menu choose the **Microsoft Defender Threat
    Intelligence (preview)** connector and click **Open Connector
    Page** at the bottom right.

![A screenshot of a computer Description automatically
generated](./media/image39.png)

4.  On the Connector page, from the **Import indicators** list, leave
    the default "**All available**" selected, and click **Connect**.

![A screenshot of a computer Description automatically
generated](./media/image40.png)

![Screenshot](./media/image41.png)

5.  The Status of the Connector should be updated to **Connected.**

![A screenshot of a computer Description automatically
generated](./media/image42.png)

6.  Threat Intelligence indicators will start being ingested into
    the **ThreatIntelligenceIndicator** table.

**Note** - We should have successfully installed all the below 4 Data
connectors.

- **Azure Activity**

- **Tenant-based Microsoft Defender for Cloud (Preview)**

- **Subscription-based Microsoft Defender for Cloud (Legacy)**

- **Microsoft Defender Threat Intelligence (preview)**
