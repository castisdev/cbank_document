
## transfer

### 활용
계좌 이체를 수행합니다.


### 요청 명세 (Body)
```
POST /cbank/api/v1/transfer
HTTP/1.1  
Content-type: application/json
```
|   Parameter  | type        |    필수    | byte |                             설명                           |
|:------------:|:-----------:|:----------:|:----:|:-----------------------------------------------------------| 
| userId|  String     |        O    |   64 | OTP를 요청한 userId  |
| sendAccountPwd|  String     |      O      |   128 | userId의 password (Base64 인코딩필요) |
| sendAccountId|  String     |      O      |   64 | 보내는 계좌의 Cbank Id |
| recvAccountId|  String     |      O      |   64 | 받는 계좌의 Id |
| amount| Long     |      O      |   32 | 이체 하는 금액 |
| transferHistory|  String     |      O      |   256 | 이체 내역 |
| memo |  String     |      O      |   256 | 메모 (이체 실패 이유, 이체 요청자 등) |
| otp|  String     |     O       |   36 | [OTP API](/cbank/api/otp.md#otp)에서 확보한 UUID 형태의 One Time Password 입니다. |

### 샘플 요청
```json
http://127.0.0.1:8080/cbank/api/v1/transfer
{
    "userId":"test1",
    "sendAccountId": "8989-0200",
    "sendAccountPwd": "dGVzdA==",
    "recvAccountId" : "8990-0200",
    "amount" : 1500,
    "transferHistory" : "test transfer tespt",
    "otp" : "1dac01eb-a76d-4ec8-9bcf-4bb77054f822",
    "memo" : "memomemo"
}
```

### 응답 명세 (Body)
```
POST
Content-type: application/json
```
|   Parameter  | Array내부        | type        |    필수    | byte |                             설명                           |
|:------------:|:-----------:|:-----------:|:----------:|:----:|:-----------------------------------------------------------| 
| resultCode  |             |  String    |    O      |   3  | 결과코드<br>200: 성공/그외 실패  |
| resultMsg   |             |   String   |   O      |   128 | 결과 메시지 |
| now         |             |   String   |  O      |   40  | 요청 시간 기록  |


### 응답 (정상 응답)
```json
{
    "resultCode": "200",
    "resultMsg": "",
    "now": "Sat Dec 9 21:58:45 KST 2021"
}
```

### 응답 (계정 ID가 없거나 비밀번호가 틀릴경우)
```json
{
    "resultCode": "400",
    "resultMsg": "not valid CBank ID or Password.",
    "now": "Sat Dec 11 21:56:57 KST 2021"
}
```

### 응답 (otp가 틀릴경우)
```json
{
    "resultCode": "400",
    "resultMsg": "not valid OTP(One Time Password).",
    "now": "Sat Dec 11 21:56:57 KST 2021"
}
```

### 응답 (해당 계좌가 존재하지 않을 경우)
```json
{
    "resultCode": "404",
    "resultMsg": "recvAccount:[8990-02001] is not exist Account!",
    "now": "Sat Dec 9 21:57:38 KST 2021"
}
```


### 응답 (잔액 부족)
```json
{
    "resultCode": "404",
    "resultMsg": "error msg: 잔액 부족 [6300739.00] < 필요 [1503333333333330]",
    "now": "Sat Dec 9 21:58:23 KST 2021"
}
```
<br>

☕ [전체 API 문서로 돌아가기](/api.md)
