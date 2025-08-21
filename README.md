# n8n-watch-tower
![n8n Watch Tower Flow](docs/flow-architecture.png)

Automated workflows built with [n8n](https://n8n.io) to integrate with the [HackerOne](https://www.hackerone.com/) API.  
This project provides an automation example for fetching HackerOne data (e.g., reports, program updates) and forwarding it to external services such as Slack or other notification channels.

## Features
- Fetch reports or events from HackerOne using API.
- Watchtower-style monitoring: get notified of new activity without manual checks.
- Easy to customize and extend with other integrations (Slack, Telegram, Email, etc.).
- Exported n8n workflows included (`.json`) for quick import.

## Project Structure
```

n8n-watch-tower/
│
├── README.md             # Project documentation
├── LICENSE               # License file (MIT by default)
├── workflows/            # Exported n8n workflows (JSON)
│   └── watchtower.json
│
├── docs/                 # Additional diagrams
│   └── flow-architecture.png

````

## Setup

1. **Clone the repository**
    ```bash
    git clone https://github.com/hackmelocal/n8n-watch-tower.git
    cd n8n-watch-tower
    ```

2. **Prepare your HackerOne API credentials**

   The workflow requires a valid **HackerOne API username** and **API token**.  
   You must encode them in **Base64** format before adding them to the workflow:

   1. Go to your [HackerOne profile settings](https://hackerone.com/settings/api_token) and generate an API token.
   2. Take your **HackerOne username** (`H1_USERNAME`) and your **API token** (`H1_API_KEY`).
   3. Combine them in the format:  
      ```
      H1_USERNAME:H1_API_KEY
      ```
   4. Encode this string in **Base64**, for example:
      ```bash
      echo -n "H1_USERNAME:H1_API_KEY" | base64
      ```
   5. Copy the encoded string and replace the placeholder in the workflow:  
      ```
      "value": "Basic BASE64(H1_USERNAME:H1_API_KEY)"
      ```

   Example:
    ```
    authorization: Basic dGVzdHVzZXI6c2VjcmV0YXBpa2V5
    ```

3. **Import workflows into n8n**

* Open your n8n instance.
* Import the JSON file(s) from `workflows/`.
* Replace the `BASE64(H1_USERNAME:H1_API_KEY)` placeholder with your Base64-encoded credentials (as described above).
* Add other credentials (Telegram bot token, Slack webhook, etc.) inside n8n.

4. **Configure Telegram notifications**

    To receive notifications via Telegram, you need to create a Telegram bot:

1. Open Telegram and search for **BotFather**.
2. Start a chat and send `/newbot`.
3. Follow the instructions to set a name and username for your bot.
4. Copy the **bot token** provided by BotFather.
5. In n8n, add this token to the Telegram node in the workflow.

5. **Run the workflow**
Once activated, the workflow will automatically monitor HackerOne and send notifications to your Telegram bot (or other configured channels).


## Notes

* This project is intended for **educational and automation purposes only**.
* Do not use it for malicious or unauthorized activity.
* Credentials should always be handled securely inside n8n.

## Future Plans

The following features are planned for upcoming releases:

* Watchtower integration with **Bugcrowd**.
* Watchtower integration with **YesWeHack**.
* Implementation of **automated testing flows** (e.g., simulated attack chains or validation steps).

## 📜 License

This project is licensed under the [MIT License](LICENSE).
