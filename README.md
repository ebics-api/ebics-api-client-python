# EBICS API Client (Python module)

<img src="./doc/ebics-api-client-logo.png" height="100" align="left" style="padding-right:20px; padding-bottom: 20px;">

Python module to utilize EBICS API Client application.  
EBICS API Client - https://sites.google.com/view/ebics-api-client  
EBICS Client can be deployed as a standalone service on a webserver or within a Docker container and provides:

<br clear="left" />

- :100: Support for EBICS Integration
- :white_check_mark: RESTful API to operate with orders, connections, keyrings, access logs, fetched files
- :white_check_mark: Extended Access Policy
- :white_check_mark: Execute order transactions directly from the App
- :white_check_mark: Manage Connections and Monitor access logs
- :white_check_mark: Scheduler Jobs, Fetched files secure storage

<br clear="left"/>

# Installation

`python3 -m pip install ebics-api-client`

# Usage

```
from ebics_api_client import ebics_api_client

client = ebics_api_client.EbicsApiClient(os.getenv('API_KEY'), os.getenv('API_HOST'))

```

# Methods

* ## Connections

Connections between client application and bank server.

| Method                             | Description                             |
|------------------------------------|-----------------------------------------|
| client.connection_create(data)     | Create new connection to the Bank.      |
| client.connection_update(id, data) | Update existing connection to the Bank. |
| client.connection_get(id)          | One connection to the Bank.             |
| client.connection_list()           | List of all connections to the Bank.    |
| client.connection_delete(id)       | Delete a connection to the Bank.        |

* ## Keyrings

Keyring with sensitive keys to perform order types methods.

| Method                            | Description                                                                                |
|-----------------------------------|--------------------------------------------------------------------------------------------|
| client.keyring_generate(data)     | Generate new keyring and encrypt by secret<br/> (Requires before INI and HIA order types). |
| client.keyring_init(data)         | Initialize keyring (Only before Bank activated connection).                                |
| client.keyring_confirm(data)      | Confirm keyring (Only after Bank activated connection).                                    |
| client.keyring_suspend(data)      | Deactivate keyring (SPR order type).                                                       |
| client.keyring_letter(data)       | Letter should be sent to Bank for Keyring activation.                                      |
| client.keyring_changeSecret(data) | Change secret for existing Keyring.                                                        |

* ## Order Types

Order type methods to download or upload files to/from the Bank.

| Method                      | Description                                                                                  |
|-----------------------------|----------------------------------------------------------------------------------------------|
| client.order_type_hev(data) | Order type methods to download or upload files to/from the Bank.                             |
| client.order_type_ini(data) | Send to the bank public signature of electronic signature.                                   |
| client.order_type_hia(data) | Send to the bank public signatures of authentication and encryption.                         |
| client.order_type_hpb(data) | Download the Bank public signatures of authentication and encryption.                        |
| client.order_type_hpd(data) | Download the bank server parameters.                                                         |
| client.order_type_hkd(data) | Download customer`s customer and subscriber information.                                     |
| client.order_type_htd(data) | Download subscriber`s customer and subscriber information.                                   |
| client.order_type_haa(data) | Download Bank available order types.                                                         |
| client.order_type_fdl(data) | Download the files from the bank.                                                            |
| client.order_type_ful(data) | Upload the files to the bank.                                                                |
| client.order_type_ptk(data) | Download transaction status.                                                                 |
| client.order_type_vmk(data) | Download the interim transaction report in SWIFT format (MT942).                             |
| client.order_type_sta(data) | Download the bank account statement.                                                         |
| client.order_type_c52(data) | Download the bank account report in Camt.052 format.                                         |
| client.order_type_c53(data) | Download the bank account statement in Camt.053 format.                                      |
| client.order_type_c54(data) | Download Debit Credit Notification (DTI).                                                    |
| client.order_type_z52(data) | Download the bank account report in Camt.052 format (i.e Switzerland financial services).    |
| client.order_type_z53(data) | Download the bank account statement in Camt.053 format (i.e Switzerland financial services). |
| client.order_type_z54(data) | Download the bank account statement in Camt.054 format (i.e available in Switzerland).       |
| client.order_type_zsr(data) | Download Order/Payment Status report.                                                        |
| client.order_type_xek(data) | Download account information as PDF-file.                                                    |
| client.order_type_cct(data) | Upload initiation of the credit transfer per Single Euro Payments Area.                      |
| client.order_type_cip(data) | Upload initiation of the instant credit transfer per Single Euro Payments Area.              |
| client.order_type_xe2(data) | Upload initiation of the Swiss credit transfer (i.e available in Switzerland).               |
| client.order_type_xe3(data) | Upload SEPA Direct Debit Initiation, CH definitions, CORE (i.e available in Switzerland).    |
| client.order_type_yct(data) | Upload Credit transfer CGI (SEPA & non SEPA).                                                |
| client.order_type_cdb(data) | Upload initiation of the direct debit transaction for business.                              |
| client.order_type_cdd(data) | Upload initiation of the direct debit transaction.                                           |
| client.order_type_btd(data) | Download request files of any BTF structure.                                                 |
| client.order_type_btu(data) | Upload the files to the bank.                                                                |

* ## Access Logs

Tracked access logs to Bank for Connections

| Method                   | Description               |
|--------------------------|---------------------------|
| client.access_log_list() | Access logs to the Banks. |

* ## Fetched files

Fetched files by run Scheduler Jobs

| Method                           | Description                                                    |
|----------------------------------|----------------------------------------------------------------|
| client.fetched_file_list()       | Fetched files of run scheduler order transactions to the Bank. |
| client.fetched_file_download(id) | Download fetched file content.                                 |
