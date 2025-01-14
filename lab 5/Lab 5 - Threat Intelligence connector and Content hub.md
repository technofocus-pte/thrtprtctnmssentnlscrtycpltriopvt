# Lab 5 - Threat Intelligence connector and Content hub

This Lab will demonstrate how to use Microsoft Sentinel Threat
Intelligence (TI) features and product integration points. During this
Lab we rely on TI data that we ingested in earlier labs, so please make
sure you have completed previous Labs. In this Lab we will also discover
how to visualize and use this data as part of investigation and
detection.

## Exercise 1 - Exploring the Microsoft Defender Threat Intelligence (Preview) connector

### Task 1 - Enabling the Microsoft Defender Threat Intelligence (Preview) connector

This connector is currently in preview and ingests Microsoft Threat
Intelligence indicators automatically into the
ThreatIntelligenceIndicator table. MDTI provides a set of indicators and
access to the <https://ti.defender.microsoft.com> portal at no
additional cost, with the premium features of the MDTI portal and API
requiring licensing.

1.  On the Azure Portal http://portal.azure.com, search for Microsoft
    Sentinel and click on **Microsoft Sentinel**.

![](./media/image1.png)

2.  Select **SwrkXXXXXXX**.

![](./media/image2.png)

3.  Click on **Data Connectors** under Configuration select **Microsoft
    Defender Threat Intelligence (Preview)**.

![](./media/image3.png)

4.  On the bottom right pane click on **Open connector page**

![](./media/image4.png)

5.  Review the data received and confirm that the connector is already
    ingesting indicators.

![](./media/image5.png)

6.  Close the **Microsoft Defender Threat Intelligence
    (Preview)** Connector page, to return to the Microsoft Sentinel home
    page.

### Task 2: Review and manage TI IOC's in Microsoft Sentinel Threat intelligence menu

After we ingested our TI data into the ThreatIntelligenceIndicator
table, our mission is to review how our SOC can leverage and manage the
TI menu to allow us to search, tag and manage the lifecycle of IOCs.

1.  On the **Microsoft Sentinel** left menu click on the **Threat
    intelligence** under Threat management. This menu is a visual
    representation of the ThreatIntelligenceIndicator table.

>  ![A screenshot of a computer Description automatically
> generated](./media/image6.png)

2.  Select one IOC from the main pane and notice that the right pane
    changed accordingly and present the metadata of the selected IOC.

![](./media/image7.png)

3.  On the top area of the main blade, we can filter the list of the
    IOC's based on a specific parameters. In our case, we only ingested
    one type of IOC (IP), but the **Type** filter allow us to filter
    based on different types. If we ingested IOC's from multiple TI data
    sources, the **source** filter allows us to slice it.

![](./media/image8.png)

### Task 3 - Review the TI data into Microsoft Sentinel Logs interface.

The ingested Indicators of Compromise (IOC) coming from any of these TI
feeds, is stored in a dedicated table
called **ThreatIntelligenceIndicator**, and visible on the Threat
Intelligence menu on the left navigation menu.

1.  On the left navigation click on **Logs**, this will redirect you to
    the Log Analytics query interface. On the query interface we can see
    on the left side the tables with the relevant fields.

![](./media/image9.png)

2.  Microsoft Sentinel built-in tables have a predefined schema, to be
    able to see the **ThreatIntelligenceIndicator** schema, run the
    following query:

ThreatIntelligenceIndicator | getschema

![](./media/image10.png)

3.  Let's explore and delve into the TI table. Run the following query
    which takes 10 records from the table:

ThreatIntelligenceIndicator | take 10

![](./media/image11.png)

4.  To understand if a specific IOC is active, we need to have a closer
    look at the following columns:

    - **ExpirationDateTime \[UTC\]**

    - **Acitve**

![](./media/image12.png)

### Task 4 - Adding new TI IOC manually in Microsoft Sentinel Threat intelligence menu

Part of the SOC analyst's job is to manually add an IOC into the TI
index from time to time. This allows other data sources and detections
to correlate and detect interaction with this IOC.

1.  On the **Threat intelligence** top menu, click on **Add new**,

![](./media/image13.png)

2.  On the **New indicator** dialog provide the below details and then
    click on **Apply** button

    - Types - **url**

    - URL - http://phishing.com

    - Tags - Click on + then type Incident 4326 click on **Apply**

    - Thread types - Click on + then
      type malicious-activity on **Apply**

    - Description - this URL is found in Incident 4326

    - Name - url indicator

    - Confidence level - uncheck the **Is null** checkbox and then set
      the vaule to **80**

    - Set the **Valid from** as today date

    - **Valid until** two weeks from today.

![](./media/image14.png)

![Screenshot](./media/image15.png)

3.  Notice to the newly created IOC on the TI menu.

![](./media/image16.png)

4.  Be aware that every new IOC added in the TI menu, will be
    automatically added to the ThreatIntelligenceIndicator table. You
    can validate it by opening the **Logs** menu and run the query
    below.

**Note** - It can take about 5 mins to have the result shown.

ThreatIntelligenceIndicator | search "http://phishing.com"

![](./media/image17.png)

5.  Select the newly created manual IOC and press **Delete** button.

![](./media/image18.png)

### Task 5 - Reviewing Analytics Rules based on Threat Intelligence data

1.  From the **Microsoft Sentinel** page, click on **Analytics** and
    then click on the **Rule Templates** tab.

![](./media/image19.png)

2.  Click on **Add filter** and then select the **Data Sources** filter.

![](./media/image20.png)

3.  Select **Microsoft Defender Threat Intelligence
    (Preview).** Click **Apply** to apply the filter.

![](./media/image21.png)

4.  As you can see, there is a long list of resulting alert templates.
    These all will correlate your different data sources with the IOCs
    present in your TI table (**ThreatIntelligenceIndicator**), to
    detect any trace of malicious indicators of compromise in your
    organization's logs.

![](./media/image22.png)

5.  As you may know, it is free to enable analytics rules in Microsoft
    Sentinel, so the best practice is to enable all the ones that apply
    to data sources that you are ingesting.

### Task 6 - Enabling Threat Intelligence Matching Analytics rule

1.  From the Microsoft Sentinel page, click on **Analytics** and click
    on **Rule Templates** tab. Clear previously applied filters if any.

![](./media/image19.png)

2.  Click on Add filter and then choose **Rule Type** filter and
    select **Threat Intelligence**.

![](./media/image23.png)

![](./media/image24.png)

3.  The resulting rule template matches Microsoft-generated threat
    intelligence data with the logs you have ingested into Microsoft
    Sentinel. The alerts are very high fidelity and are turned ON by
    default. Visit this link for more information about this type of
    rule.

![](./media/image25.png)

4.  Select the rule template and notice the different data sources that
    are supported (at the time of writing, these are CEF, Syslog and
    DNS). Click on **Create rule**.

![](./media/image26.png)

5.  In the wizard, click on **Review and Create**.

![](./media/image27.png)

6.  Click on the **Save** button to create the Rule

![](./media/image28.png)

![Screenshot](./media/image29.png)

### Task 7 - Explore and visualize Threat Intelligence workbook

1.  While still on the **Microsoft Sentinel** page, click
    on **Workbooks** under **Threat management** and then click on **Add
    workbook**.

![](./media/image30.png)

2.  You will find some pre-built visualizations that show you the
    indicators imported into Sentinel over time, by type and provider.
    To modify or add a new chart, select the **Edit** button at the top
    of the page to enter editing mode for the workbook.

![](./media/image31.png)

3.  Add a new chart of threat indicators by threat type. To do this,
    scroll to the very bottom of the page and select **Add** \> **Add
    Query**.

![](./media/image32.png)

4.  Add the following text to the Log Analytics workspace Log Query text
    box and then click on the **Run Query** button.

ThreatIntelligenceIndicator | summarize count() by ThreatType

![](./media/image33.png)

5.  In the Visualization drop-down, select **Bar chart**.

![a bar chart ](./media/image34.png)

6.  Select the **Done editing** button. You've created a new chart for
    your workbook.

![](./media/image35.png)

7.  Click on the **Save** button and on the Workbook details tab,
    provide the Resource group details and then click on
    the **Apply** button.

![](./media/image36.png)

![Screenshot](./media/image37.png)

## Exercise 2 - Exploring the Microsoft Sentinel Content hub.

### Task 1 - Overview of Microsoft Sentinel Content hub

1.  On the Azure Portal http://portal.azure.com, search for Microsoft
    Sentinel and click on **Microsoft Sentinel**.

![](./media/image38.png)

2.  Select **SwrkXXXXXXX**.

![](./media/image39.png)

3.  Now click **Content hub** under **Content Management**.

![](./media/image40.png)

4.  In the search bar, type Cloudflare You will see a single result
    corresponding to Cloudflare solution. You could also search using
    the filtering options at the top.

![](./media/image41.png)

5.  Select the Cloudflare solution. As you can see on the right pane,
    here we have information about this solution, like category,
    pricing, content types included, solution provider, version and also
    who supports it. Click **Install**.

![](./media/image42.png)

![](./media/image43.png)

6.  Click on the **Manage** button.

![](./media/image44.png)

7.  Notice the different artifacts that are included in this
    solution: **Data Connector, Parser, Workbook, Analytics
    Rules** and **Hunting Queries**. Each Solution can contain a
    different set of artifacts.

![](./media/image45.png)

8.  Close the **Cloudflare for Microsoft Sentinel** information page and
    you can navigate to other solutions. In the next exercise, we will
    install one of them.

### Task 2 - Deploying a new solution from Content hub

1.  From the Microsoft Sentinel portal, navigate to **Content
    hub** under **Content Management**

![](./media/image46.png)

2.  In the search bar, type dynamics 365 CE. Select on the **Dynamics
    365 CE Apps** solution and click on **View Details**. Notice the
    content being added by this solution (Data Connector, Analytics
    Rules, Workbook, Hunting Queries and Watchlists).

![](./media/image47.png)

**Note**: if **Dynamics 365 CE Apps** is unavailable, then install **Microsoft Business Applications** and continue with the rest of the exercise.

![image](https://github.com/user-attachments/assets/674fd21c-63ed-4b48-bca2-b2f0c6b24bb4)


3.  Click on **Create**.

![](./media/image48.png)

4.  On the **Create Microsoft Sentinel Solution for Dynamics 365 CE Apps
    (Preview)** page provide the below details.

a\. Subscription - **Azure Pass - Sponsorship**

b\. Resource group - **RG4Sentinel**

c\. Workspace - **SwrkXXXXXX**

![](./media/image49.png)

5.  Click on **Next** and review the information on
    the **Workbooks** tab.

![](./media/image50.png)

6.  Click on **Next:** and review the information on **Analytics** tab.

![](./media/image51.png)

7.  Notice the different **Analytics Rules** that will be added to your
    workspace. Click **Next.**

![](./media/image52.png)

8.  On the **Hunting Queries** tab, notice the Hunting Queries included
    in the solution. Click **Review + create**.

![](./media/image53.png)

9.  A final validation will run. If everything is ok, click
    on **Create** button. The deployment will kick off and finish in a
    few seconds.

![](./media/image54.png)

![](./media/image55.png)

### Task 3 - Reviewing and enabling deployed artifacts

1.  Navigate back to **Microsoft Sentinel** home page and click
    on **Analytics**, and select the **Rule Templates** tab.

![](./media/image56.png)

2.  Type Dynamics in the search box. You should see **16** different
    analytics rules that look at **Dynamics 365 data**.

![](./media/image57.png)

3.  Notice that these rules are available as **templates**. In a
    real-world environment, you would need to create them in order to
    use them.

4.  Navigate to **Workbooks** under Threat Management.
    Select **Templates** search for Dynamics Like the analytics rules
    the workbook exists as a template. This should be empty unless you
    have enabled the Dynamics 365 connector.

![](./media/image58.png)

5.  Navigate to **Hunting**, go to **Queries** tab and search
    for dynamics 365 You should see 2 new queries that use data coming
    from Dynamics 365.

![](./media/image59.png)

6.  Navigate to **Watchlist** under Configuration. Search for d365.
    Notice you have two new watchlists.

![](./media/image60.png)

**Congratulations!!!**, you have completed Lab 5!
