
## Login Check

### 활용
보안 거래를 위한 유저 ID와 Password를 확인합니다.


### 요청 명세 (Body)
```
POST /cbank/api/v1/login 
HTTP/1.1  
Content-type: application/json
```
|   Parameter  | type        |    필수    | byte |                             설명                           |
|:------------:|:-----------:|:----------:|:----:|:-----------------------------------------------------------| 
| userId|  String     |    O        |   64 | Login을 요청하는 userId  |
| encodedPassword|  String     |    O        |   128 | Login을 요청하는 password (Base64 인코딩필요)  |
| companyId|  String     |  O          |   128 | CBank와 사전에 협의된 B2B용 Id |

### 샘플 요청
```json
http://127.0.0.1:8080/cbank/api/v1/login
{
    "userId":"test",
    "encodedPassword":"dGVzdA==",
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

> #### ⚠ 응답항목  
> login Check는 castis bank에 로그인 가능한 user인지 확인하는 용도로 사용합니다.<br>
> 과도하게 같은 아이디로 여러번 틀릴 경우 해당 ID가 이용 불가가 될 수 있습니다.<br>

### 응답 (Login 성공)
```json
{
    "resultCode": "200",
    "resultMsg": "",
    "now": "Mon Dec 06 21:41:56 KST 2022",
}
```

### 응답 (userId 가 존재하지 않을 경우)
```json
{
    "resultCode": "400",
    "resultMsg": "[test] is not exist User!",
    "now": "Mon Dec 06 21:42:14 KST 2022",
}
```

### 응답 (인가되지 않은 companyId일 경우)
```json
{
    "resultCode": "400",
    "resultMsg": "[test] is not valid Company!",
    "now": "Mon Dec 06 21:46:03 KST 2022",
}
```

### 응답 (Password가 틀릴 경우)
```json
{
    "resultCode": "400",
    "resultMsg": "[test] not valid encoded password!",
    "now": "Mon Dec 06 21:46:03 KST 2022",
}
```
<br>

☕ [전체 API 문서로 돌아가기](/api.md)
