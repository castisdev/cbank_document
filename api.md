## URI 목록	
CBank Open API 목록 입니다.

```bash
Authorization : OTP (One Time Password)
Content-Type : application/json
```

|              API            |     Method    |               Endpoint              |
|:---------------------------:|:-------------:|:-----------------------------------|
|[ping](/cbank/api/ping.md#ping)      |      `GET`     |     /cbank/api/v1/ping                |
|[User check](/cbank/api/userCheck.md#user-check)    |      `GET`     |     /cbank/api/v1/user/{companyId}/{userId}  |
|[Login check](/cbank/api/loginCheck.md#account-history)    |      `POST`     |     /cbank/api/v1/login  |
|[Account list](/cbank/api/accountList.md#account-list)    |      `GET`     |     /cbank/api/v1/accounts/{companyId}/{accountId}  |
|[Account Info](/cbank/api/accountInfo.md#account-info)    |      `GET`     |     /cbank/api/v1/account/info/{companyId}/{accountId}  |
|[Account Name](/cbank/api/accountName.md#account-name)    |      `GET`     |     /cbank/api/v1/accountnames/{companyId}/{accountId}  |
|[Account Details](/cbank/api/accountDetails.md#account-name)    |      `GET`     |     /cbank/api/v1/accountdetails/{companyId}/{accountId}  |
|[otp](/cbank/api/otp.md#otp)    |      `POST`     |     /cbank/api/v1/otp  |
|[Account History](/cbank/api/accountHistory.md#account-history)    |      `POST`     |     /cbank/api/v1/account/history  |
|[Transfer](/cbank/api/transfer.md#transfer)    |      `POST`     |     /cbank/api/v1/transfer  |
