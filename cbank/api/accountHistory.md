
## Account history

### 활용
계좌의 거래 내역을 요청하여 받아옵니다.


### 요청 명세 (Body)
```
POST /cbank/api/v1/account/history
HTTP/1.1  
Content-type: application/json
```
|   Parameter  | type        |    필수    | byte |                             설명                           |
|:------------:|:-----------:|:----------:|:----:|:-----------------------------------------------------------| 
| userId|  String     |        O    |   64 | OTP를 요청하는 userId  |
| accountId|  String     |      O      |   64 | 계좌의 Id |
| duration|  String     |       △     |   64 | 요청하는 기간을 설정합니다.(Y, M, D 사용가능)<br>예: 1Y (1년치)<br>3M (3개월치)<br>기본값:1M(1개월치) |
| startDate|  String     |      △     |   64 | 요청하는 시작 기간을 설정합니다.(YYYYMMDD사용가능)<br>예: 20211221|
| endDate|  String     |    X    |   64 | 요청하는 종료 기간을 설정합니다. 설정하지 않을 경우 오늘입니다. (YYYYMMDD사용가능)<br>예:20211221|
| otp|  String     |     O       |   36 | [OTP API](/cbank/api/otp.md#otp)에서 확보한 UUID 형태의 One Time Password 입니다. |

> #### ⚠ duration, startDate, endDate  
> 기본적으로는 duration 설정이 가장 우선 순위가 높습니다. (duration 설정이 있으면 startDate, endDate는 무시됩니다.)<br>
> duration 설정이 없을 경우 startDate와 endDate를 이용하여 처리 됩니다.<br>
> duration 설정이 없을 경우 endDate의 기본값은 오늘이며, startDate가 없으면 오류가 발생합니다.
> 즉, duration이나 startDate 두 item중 하나는 명시적으로 설정하시기를 권고 드립니다.


### 샘플 요청
```json
http://127.0.0.1:8080/cbank/api/v1/account/history
{
    "userId":"teatime",
    "accountId": "1234-0200",
    "duration" : "1M",
    "otp" : "20d9b5a9-ee34-4409-a7a1-4aa9d0273efd"
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
| count       |             |    int     |  O      |  10 | 전체 조회 이력 개수   |
| history     |             |    Array   | O      |   | 실제 이체 내역을 배열 형태로 반환 |
|             |      id     |    String  |   O      |  10 |  이체 내역 ID  |
|             |      type     |   String   |   O      |  10 |  이체 Type<br>Internal:내부이체<br>External:외부이체<br>salary:급여이체  |
|             |      sendName     |    String  |   O      |  64 | 보내는 계좌 이름 |
|             |      sendAccount     |    String  |   O      |  64 | 보내는 계좌 번호 |
|             |      recvName     |    String  |   O      |  64 | 받는 계좌 이름 |
|             |      recvAccount     |    String  |   O      |  64 | 받는 계좌 번호 |
|             |      history     |    String  |   O      |  128 | 이체 내역 |
|             |      amount     |    String  |   O      |  64 | 이체된 금액 |
|             |      balace     |    String  |   O      |  64 | 이체 후 잔액 |
|             |      date     |    String  |   O      |  20 | 이체 일시 |
|             |      status     |    String  |   O      |  36 | 이체 결과 |
|             |      memo     |    String  |   O      |  256 | 메모 (이체 실패 이유, 이체 요청자 등) |


### 응답 (정상 응답)
```json
{
    "resultCode": "200",
    "resultMsg": "",
    "now": "Mon Dec 06 21:54:22 KST 2021",
    "count": 2,
    "history": [
        {
            "id": "34",
            "type": "Internal",
            "sendName": "퇴근후티타임 사업부",
            "sendAccount": "0379-0200",
            "recvName": "테스트",
            "recvAccount": "0001-0789",
            "history": "테스트_이력_1",
            "amount": "360000.00",
            "balance": "33.00",
            "date": "2021-12-03 11:27:48.0",
            "status": "Success",
            "memo": "신청자:teatime"
        },
        {
            "id": "68825",
            "type": "Internal",
            "sendName": "퇴근후티타임 사업부",
            "sendAccount": "0379-0200",
            "recvName": "내부이체수수료_원화",
            "recvAccount": "0002-0100",
            "history": "테스트_이력_2",
            "amount": "50.00",
            "balance": "21.00",
            "date": "2021-12-03 11:27:49.0",
            "status": "Success",
            "memo": "신청자:teatime"
        }
    ]
}
```

### 응답 (otp가 틀릴경우)
```json
{
    "resultCode": "400",
    "resultMsg": "not valid OTP(One Time Password).",
    "now": "Mon Dec 06 21:57:18 KST 2021",
    "count": 0,
    "history": []
}
```

### 응답 (해당 계좌가 userId의 계좌가 아닐 경우)
```json
{
    "resultCode": "400",
    "resultMsg": "[0379-0202] is not among [test]",
    "now": "Mon Dec 06 21:57:52 KST 2021",
    "count": 0,
    "history": []
}
```
<br>

☕ [전체 API 문서로 돌아가기](/api.md)
