
## OTP

### 활용
보안 거래를 위한 OTP (One Time Password)를 획득 합니다.


### 요청 명세 (Body)
```
POST /cbank/api/v1/otp 
HTTP/1.1  
Content-type: application/json
```
|   Parameter  | type        |    필수    | byte |                             설명                           |
|:------------:|:-----------:|:----------:|:----:|:-----------------------------------------------------------| 
| userId|  String     |    O        |   64 | OTP를 요청하는 userId  |
| companyId|  String     |  O          |   128 | CBank와 사전에 협의된 B2B용 Id |

### 샘플 요청
```json
http://127.0.0.1:8080/cbank/api/v1/otp
{
    "userId":"test",
    "companyId":"test_app"
}
```

### 응답 명세 (Body)
```
POST
Content-type: application/json
```
|   Parameter  | type        |    필수    | byte |                             설명                           |
|:------------:|:-----------:|:----------:|:----:|:-----------------------------------------------------------| 
| resultCode  |  String     |     O      |   3  | 결과코드<br>200: 성공/그외 실패  |
| resultMsg   |  String     |     O      |   128 | 결과 메시지 |
| now |  String     |     O      |   40  | 요청 시간 기록  |
| otp   |  String     |     O      |   36  | UUID 형태의 One Time Password 입니다.  |

> #### ⚠ 응답항목  
> otp는 단 1회만 사용할 수 있습니다.<br>
> 다른 보안 요청 이후 다시 보안 요청이 필요하면 otp를 다시 발급 받아야합니다.<br>
> 발급된 otp의 유효시간은 1분(60초) 입니다.<br>

### 응답 (정상 발급)
```json
{
    "resultCode": "200",
    "resultMsg": "",
    "now": "Mon Dec 06 21:41:56 KST 2021",
    "otp": "9843ed89-f4a7-420c-af65-2924e3b7afb7"
}
```

### 응답 (userId 가 존재하지 않을 경우)
```json
{
    "resultCode": "400",
    "resultMsg": "[test] is not exist User!",
    "now": "Mon Dec 06 21:42:14 KST 2021",
    "otp": ""
}
```

### 응답 (인가되지 않은 companyId일 경우)
```json
{
    "resultCode": "400",
    "resultMsg": "[test] is not valid Company!",
    "now": "Mon Dec 06 21:46:03 KST 2021",
    "otp": ""
}
```

<br>

☕ [전체 API 문서로 돌아가기](/api.md)
