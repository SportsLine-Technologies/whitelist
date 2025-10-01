# Whitelist System

This directory contains the whitelist system for the testnet faucet.

## Files

- `users.csv` - CSV file containing whitelisted usernames
- `README.md` - This documentation file

## CSV Format

The `users.csv` file must have the following format:

```csv
username
3E810860877E2D
3A810860877E93
```

### Fields:
- `username` - The username to whitelist (required, this has to be userID from the database, e.g., 3E810860877E9D)

## Adding Users
To add a user to the whitelist:

1. Open `users.csv`
2. Add a new line with the username
3. Save the file
4. The system will automatically pick up the changes
5. Alternatively, upload a new users.csv file to replace the existing one

It will take around 15 minutes for those changes to reflect on the frontend, but you can immediately validate the format of the file (see below).

## Validate users.csv format

After saving the new version of users.csv, check:

```
http://predictex.io/api/validate-whitelist
```

Verify that isValid is true and that the userCount is accurate:

```json
{
  "isValid": true,
  "userCount": 5,
  "usernames": [
    "test_user",
    "demo_user",
    "sample_user",
    "3E1C90A94746AE",
    "3E810860877E9D"
  ],
  "errors": [],
  "csvContent": "username\ntest_user\ndemo_user\nsample_user\n3E1C90A94746AE\n3E810860877E9D\n",
  "timestamp": "2025-10-01T18:53:58.122Z",
  "source": "github"
}
```


## API Endpoint

The whitelist endpoint is available as a next.js app route at:
```
GET /api/isWhitelisted?username={username}
```

Response:
```json
{
  "isWhitelisted": true,
  "username": "testuser1",
  "timestamp": "2024-01-01T00:00:00.000Z"
}
```

Unlike the validation endpoint, this endpoint uses a cache, app users will only get updates around 15 minutes after the users.csv file has been updated.
