# Whitelist System

This directory contains the whitelist system for the testnet faucet.

## Files

- `users.csv` - CSV file containing whitelisted usernames
- `README.md` - This documentation file

## CSV Format

The `users.csv` file must have the following format:

```csv
username
testuser1
testuser2
```

### Fields:
- `username` - The username to whitelist (required)
- `added_date` - Date when user was added (YYYY-MM-DD format)
- `added_by` - Who added the user (admin identifier)

## Adding Users

To add a user to the whitelist:

1. Open `users.csv`
2. Add a new line with the username
3. Save the file
4. The system will automatically pick up the changes
5. Alternatively, upload a new users.csv file to replace the existing one

## API Endpoint

The whitelist check is available as a next.js app route at:
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
