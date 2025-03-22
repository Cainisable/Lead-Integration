# Lead-Integration
A pipeline I built for a client to import leads and synchronize incoming leads across multiple platforms. 

_Please note that no JSON blueprints are available for this automation flow._


### 🤖 External API Integrations Used:
- Hubspot
- Gmail
- Klaviyo
- Apollo
- Google Contacts
- Google Sheets
- Chatgpt


### ✨ Features:
- Takes in new leads, prepares the data, and creates integrated profiles between each platform.
- Handles the initial email communication, with automated follow-up emails.
- Analyzes the customer and categorizes them in the system
- Automated Apollo information enrichment for corporate clients.

### 🌊 The Flow:
1. **Lead Data Recording**

2. **Lead Importing**

3. **Data Enrichment**

  
# Pipeline Breakdowns:
_Please note that in interest of space, the pipelines have been compressed to fit a single screen_
      
### 1. Lead Recording
![Bark Lead Import](https://github.com/user-attachments/assets/5cf31c7f-4fea-4c01-a6e8-582d29e3b079)

The primary lead source we work with is Bark. Bark has direct integration into Zapier so this is the first step. We import the lead into sheets, and then trigger a webhook for our first Make Scenario.

![Bark Lead Recording](https://github.com/user-attachments/assets/7abd7a78-0014-4649-9907-02e36393ba28)

While this particular flow is built for Bark leads, the next steps could be triggered by any lead, as the automation is built to work for any source as long as we have the necessary data. The Bark flow here utilizes regular expressions to grab the different variables. If the formatting is standard it does this with just one, but if it is not, a more intensive data gathering process takes place, in order to collect whatever information it can. At the end of this scenario, it triggers the webhook for the next step of the pipeline.
    

### 2. Instant Lead Import
![Instant Lead Import](https://github.com/user-attachments/assets/cc69243f-0fa7-4872-99fd-4ebe6b667740)

This flow is the bread and butter of the automation. It is built for any lead type (as long as we gather the correct data). It's relatively linear, and runs as such:

1. The data we need is gathered into variables for easy mapping
2. We import the client into Google Contacts for easy importing into Zoom.
3. The client is imported into Klaviyo, and depending on their request, they are sorted into different categories so we can send them the correct email types.
4. Next, we create the Hubspot. We start with the deal, and then the contact and include all the details within a note attached to the profile.
5. Based on the information gathered previously, different labels are applied to the contact.
6. If it's a corporate client, we utilize Apollo to grab additional information.
7. Depending when the lead came in, it creates a task for either the same day, or the next business day for us to contact them.
8. An email is sent to the client immediately.

Due to using webhooks and instant triggering of the Bark to Zapier integration, this gives a near instantaneous process of the lead purchasing to the first email to the client.

### 3. Apollo Enrichment

This part of the process starts as we finish importing the lead into Hubspot in the previous step. Due to how the Apollo API works, it takes place over two scenarios:

![Apollo Info Import](https://github.com/user-attachments/assets/b8d42d80-0a56-432f-b405-3e3955109d44)

- The first step is to request a person enrichment. This let's us gather their information, such as their company, and in some cases, additional emails (including personal contacts in some cases).
- Due to how Apollo's API functions, a request is put in for the client's phone number.

![Apollo Phone Hook](https://github.com/user-attachments/assets/24fe5d4d-1449-49ad-a818-d0b162765b69)

- The next step triggers automatically once Apollo has finished. If it's successfuly the info is recorded and their profile on Hubspot and Klaviyo is updated. 
