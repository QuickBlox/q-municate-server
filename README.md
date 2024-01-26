# Q-Municate Server

Q-Municate Server is designed for secure storage of API keys using dotenv.
This server allows you to create a QuickBlox user session using Firebase Authentication with Phone Numbers.
It also redirects requests to an Open AI API.

## Prerequisites

- Node.js (v16 and above)
- npm (v8 and above)

## Installation

Install dependencies:

```bash
npm install
```

## Configurations

Set up environment variables:

1. Rename the `.env.example` file to `.env`.
2. Edit the `.env` file and replace the placeholder values with your actual configuration.

## Usage

To start the server, run the following command:

```bash
npm start
```

The server will be started on the specified port (or default port 3000 if not provided).

### Create QuickBlox session

To create a QuickBlox user session, submit a `POST` request to the `/session` endpoint with the `access_token` received from Firebase.

```bash
curl --request POST \
  --url http://localhost:3000/session \
  --header 'Content-Type: application/json' \
  --data '{
	"access_token": "<FIREBASE_TOKEN_ID>"
}'
```

### Open AI Proxy

To submit requests to Open AI, you no longer need to send an API Key.
You only need to pass the QB-Token header with the QuickBlox user session,
and the server will redirect your request to OpenAI.

```bash
curl --request GET \
  --url http://localhost:3000/v1/models \
  --header 'QB-Token: <QB_SESSION_TOKEN>'
```

## QuickBlox

Q-Municate Server required integration with QuickBlox to establish a secure access mechanism for the Open AI API and Firebase authorization. By incorporating QuickBlox, a double authentication process is implemented to guarantee that only authorized users can gain access to the API. This involves verifying the registration and authorization of the user attempting to access the API, effectively thwarting any unauthorized third-party interference and safeguarding the API against potential attackers.

To integrate QuickBlox into the Q-Municate Server, follow these steps:

1. Register and set up your QuickBlox account by following the instructions provided in the QuickBlox [documentation](https://docs.quickblox.com/docs/introduction).

2. Obtain your QuickBlox API URL and ensure that these it is correctly configured in the `.env` file.

## Contributing

Contributions are welcome! If you find any issues or want to add new features, please open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).
