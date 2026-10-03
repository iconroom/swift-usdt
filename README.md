# SWIFT / Wire to USDT Live Bridge Engine

This package contains the backend engine designed to simulate and handle the automated workflow between traditional banking wire/SWIFT notifications and digital USDT stablecoin settlements.

## Project Structure
- `main.py`: The core FastAPI application, SQLite ledger database, and background transaction worker.
- `requirements.txt`: Python package dependencies.
- `ledger.sqlite`: Automatically created local ledger database that tracks incoming transfers and payouts.

---

## Setup & Execution Guidelines

### Step 1: Install Dependencies
Open your terminal inside the project directory and run:
```bash
pip install -r requirements.txt
```

### Step 2: Start the Engine Server
Run the FastAPI server locally:
```bash
python main.py
```
The server will start running at `http://localhost:8000`. You can also access the interactive documentation UI at `http://localhost:8000/docs`.

### Step 3: Test the Webhook (Simulating a SWIFT Wire Transfer)
Open a separate terminal window and dispatch a test cURL command mimicking an incoming bank clearance notice:

```bash
curl -X POST "http://localhost:8000/api/v1/webhook/swift-deposit" \
-H "Content-Type: application/json" \
-d '{
  "transaction_ref": "UETR-SWIFT-2026-998811",
  "sender_name": "Apex International Trade Corp",
  "fiat_amount": 25000.00,
  "fiat_currency": "USD",
  "target_wallet": "TV9zQAbCdeF...YourUSDTWallet...XYZ"
}'
```

### Step 4: Check Transaction Ledger Status
You can check the live audit state of any processed transaction reference at any time via:
```bash
curl "http://localhost:8000/api/v1/ledger/status/UETR-SWIFT-2026-998811"
```
