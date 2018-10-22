## Dialogflow Fulfillment with Telephony, Google Sheets API, and Slot Filling

The following is a restaurant reservation sample that involves interacting with the restaurant's agent through a provided Dialogflow Telephony Gateway phone number in order to make a reservation and alternatively, the user can opt to have a call be placed to the restaurant's main line. This sample will highlight certain Telephony features that can bring more depth and substance to a typical agent.

Telephony features:
    + Synthesize speech for SSML support
    + Playing audio
    + Call transfers

The reservation data will be saved using the Google Sheets API. In addition, slot filling simplifies your agent by letting you obtain multiple, required parameters within a single intent as well as automatically managing contexts via output contexts. If any parameters are missing from a user utterance, your agent will automatically prompt users for the required parameters.

## Setup

Select **only one** of the options below.

### Option 1: Add to Dialogflow (Recommended)
To create this agent from our template:

<a href="https://console.dialogflow.com/api-client/oneclick?templateUrl=https://oneclickgithub.appspot.com/dialogflow/fulfillment-telephony-nodejs&agentName=TelephonyReservations" target="blank">
  <img src="https://dialogflow.com/images/deploy.png">
</a>

### Option 2: Firebase CLI
1. Create a [Dialogflow Agent](https://console.dialogflow.com/).
2. `git clone https://github.com/dialogflow/fulfillment-telephony-nodejs.git`
3. Go to **Settings** ⚙ > **Export and Import** > **Restore from zip** using the `dialogflow-agent.zip` in this directory.
4. `cd` to the `functions` directory
5. Run `npm install`.
6. Install the Firebase CLI by running `npm install -g firebase-tools`
7. Login with your Google account, `firebase login`
8.  Add your project to the sample with `firebase use <project ID>`
  + In Dialogflow console under **Settings** ⚙ > **General** tab > copy **Project ID**.
9. Run `firebase deploy --only functions:dialogflowFulfillment`
10. Back in Dialogflow Console > **Fulfullment** > **Enable** Webhook.
11. Paste the URL from the Firebase Console’s events column into the **URL** field > **Save**.

## Configuration
#### Service Account Authentication with JWT/OAuth 2.0
1. From the [Dialogflow's console](https://console.dialogflow.com) > go to **Settings ⚙** and under the `General` tab > go the `Project Id` link, which will take you to the **Google Cloud Platform** console
2. In the Cloud console, go to **Menu ☰** > **APIs & Services** > **Library**
3. Select **Google Sheets API** > **Enable**
4. Under **Menu ☰** > **APIs & Services** > **Credentials** > **Create Credentials** > **Service Account Key**.
5. From the dropdown, select **New Service Account**
    + name:  `telephony-sample`
    + role:  **Project/Owner**
    + key type: **JSON** > **Create**
    + JSON file will be downloaded to your local machine

#### Adding Service Account Details to Agent and a Google Sheet
1. From your preferred Google Drive account, create a new spreadsheet and **Share** with the service account email
    + Should resemble `telephonyfulfillment@telephonysample.iam.gserviceaccount.com`
    + To find the Service account email, look in the private JSON file > **client_email**
2. In the Dialogflow console > **Fulfillment** section > replace `line 26` with the private JSON contents and `line 56` with the service account-shared spreadsheetId.
    + You can find the spreadsheetId from the Google Sheets URL:       `https://docs.google.com/spreadsheets/d/<SPREADSHEETID>/`

#### Getting a Dialogflow Telephony Gateway Phone Number
1. From **Settings ⚙** > **General** tab > **Enable Beta features and APIs** > **Save**
2. Go to the **Integrations** section >
      + Select an Area Code (optional) > **Next** > Choose a number
      + You can always view your agent's number by visiting **Integrations > Dialogflow Telephony Gateway**

#### Testing this Sample
1. From the Dialogflow console, replace all the phone numbers in the Telephony `Call transfer` responses to a number that you can ensure it is working as expected.
2. Add the following columns to your Google Sheet (A1 to E1): `Date`, `Time (24HR)`, `Name`, `Group`, `Number`
3. Now you can test out this sample by calling the Dialogflow Telephony agent's number at `+1 415-582-6862`.

#### Adding Audio Files to Agent (Optional)
For Telephony's playing audio files feature, you can use VLC in order to properly reformat a given .wav file with the following steps:
1. **File > Convert/Stream**
2. **Choose Profile > Audio CD > Customize > Audio codec**
      + WAV
      + Bitrate = 16
      + Channels = 1
      + Samplerate = 8000 > **Apply** > **Save as File**

3. Upload this file through **Google Cloud Platform** console > **Menu ☰** > **Storage** > **Browser** > select a bucket link and upload your audio file.
4. Back in the Dialogflow console, you can now add Telephony `Play audio` responses with the following format:
      + Generally: `gs://<bucket>/<object>`
      + Ex: `gs://telephonysample.appspot.com/gcloud-multi.wav`

## Related Samples
| Name       | Language           |
| ------------- |:-------------:|
| [Fulfillment & Regex Validation](https://github.com/dialogflow/fulfillment-regex-nodejs)      | Node.js |
| [Weather: Fulfillment & WWO API](https://github.com/dialogflow/fulfillment-weather-nodejs)     | Node.js      |  
| [Basic Slot Filling](https://github.com/dialogflow/fulfillment-slot-filling-nodejs) | Node.js |
| [Bike Shop: Fulfillment & Google Calendar API](https://github.com/dialogflow/fulfillment-bike-shop-nodejs)| Node.js |
| [Temperature Trivia: Fulfillment & Actions on Google](https://github.com/dialogflow/fulfillment-temperature-converter-nodejs) | Node.js |
| [Fulfillment & Actions on Google](https://github.com/dialogflow/fulfillment-actions-library-nodejs) | Node.js |
| [Fulfillment & Firestore Database](https://github.com/dialogflow/fulfillment-firestore-nodejs) | Node.js |
| [Multi-language/locale](https://github.com/dialogflow/fulfillment-multi-locale-nodejs) | Node.js |

For Fulfillment Webhook [JSON Requests & Responses](https://github.com/dialogflow/fulfillment-webhook-json).


## References & Issues
+ Questions? Try [StackOverflow](https://stackoverflow.com/questions/tagged/dialogflow),  [Dialogflow Help Forum](https://productforums.google.com/forum/#!forum/dialogflow), or [Support](https://dialogflow.com/support).
+ For bugs, please report an issue on [Github](https://github.com/dialogflow/dialogflow-fulfillment-nodejs/issues).
+ Dialogflow [Documentation](https://docs.dialogflow.com).
+ Dialogflow [Fulfillment Classes Reference](https://github.com/dialogflow/dialogflow-fulfillment-nodejs/tree/master/docs).
+ For more info on the [Actions on Google NPM module](https://github.com/actions-on-google/actions-on-google-nodejs)
+ For more info on [Building Actions on Google with Dialogflow Agents Documentation](https://developers.google.com/actions/dialogflow/)

## Make Contributions
Please read and follow the steps in the CONTRIBUTING.md

## License
See LICENSE.md

## Terms
Your use of this sample is subject to, and by using or downloading the sample files you agree to comply with, the [Google APIs Terms of Service](https://developers.google.com/terms/) and [Dialogflow's Terms of Use and Privacy Policy](https://dialogflow.com/terms-and-privacy).
