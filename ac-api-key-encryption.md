---

copyright:
  years: 2025
lastupdated: "2025-08-08"

keywords: app-configuration, app configuration, encrypt api key
subcollection: app-configuration

---
{{site.data.keyword.attribute-definition-list}}

# Encrypted APIKey Requirement
{: #encrypted-apikey-requirement}

The `ibm-appconfiguration-js-client-sdk` and `ibm-appconfiguration-react-client-sdk` now requires users to provide an **Encrypted Client SDK APIKey** instead of the plain text APIKey to enhance security. This helps prevent exposure of the APIKey when inspecting the webpage through browsers.

To provide maximum security, we utilize a random nonce during the encryption process. As a result, each time you encrypt your APIKey, the encrypted value will be different, but the underlying plain text remains the same when it is decrypted during authentication.

## Steps to Generate and Use Encrypted Client SDK APIKey
{: #ac-generation-apikey}

1. Obtain Your Plain APIKey:
    - Navigate to the **Service Credentials** section of your {{site.data.keyword.appconfig_short}} instance on the IBM Cloud dashboard.
    - Generate a **`Client SDK`** role APIKey and copy the apikey from the service credentials.
2. Encrypt Your APIKey:
    - Use the following API endpoint to encrypt your plain APIKey
        ```code
        POST /apprapp/feature/v1/instances/<guid>/encrypt
        ```

        Example: `https://eu-gb.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/720f9034-c990-4305-96d6-4f65ffacef2c/encrypt`
    - In the body of the request, include your plain APIKey as follows:
        ```code
        {
          "client_sdk_apikey": "your_plain_apikey"
        }
        ```

    - The response will contain your AES-256 encrypted APIKey.
3. Updating your code:

  **Javascript SDK:**
     Update Your Initialization Code:
    - Replace the use of the plain APIKey in your application with the encrypted APIKey. Below is an updated example of how to initialize the SDK using the encrypted APIKey:
        ```js
        const region = AppConfiguration.REGION_US_SOUTH; // Specify your region
        const guid = '<guid>'; // Instance ID from Service Credentials
        const apikey = '<encrypted_apikey>'; // Use the encrypted APIKey

        const collectionId = 'airlines-webapp'; // Your collection ID
        const environmentId = 'dev'; // Your environment ID

        const appConfigClient = AppConfiguration.getInstance();

        async function initialiseAppConfig() {
            appConfigClient.init(region, guid, apikey); // Initialize with encrypted APIKey
            await appConfigClient.setContext(collectionId, environmentId);
        }

        try {
            await initialiseAppConfig();
            console.log("App configuration SDK initialized successfully");
        } catch (e) {
            console.error("Failed to initialize app configuration SDK", e);
        }
        ```

   **React SDK:**
     Update Your AppConfigProvider Code:
    - Replace the use of the plain APIKey in your application with the encrypted APIKey. Below is an updated example of how to initialize the SDK using the encrypted APIKey:
        ```js
        import { withAppConfigProvider } from 'ibm-appconfiguration-react-client-sdk';

        (async () => {
        const AppConfigProvider = await withAppConfigProvider({
            region: 'us-south', // Specify your region
            guid: '<guid>', // Instance ID from Service Credentials
            apikey: '<encrypted_apikey>', // Use the encrypted APIKey
            collectionId: 'airlines-webapp', // Your collection ID
            environmentId: 'dev' // Your environment ID
        })

        ReactDOM.render(
            <AppConfigProvider>
                <YourApp />
            </AppConfigProvider>,
            document.getElementById('root')
        );
        })();
        ```

## Existing Users: Update Required
{: #ac-existing-users-update}

If you are already using a plain APIKey, update your application to generate and use the encrypted APIKey as per the previous steps.
