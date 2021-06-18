# bigquantAPI
模拟交易API使用说明
API 的请求格式
https://bigquant.com/bigwebapi/algo_info/planned_orders

( 1 ) HTTP请求方式
POST

( 2 ) 参数说明
参数	类型	必须	说明
id_list	string	否	策略ID, 支持id和notebook_id，用;分开。
不填则返回全部正在运行的自己和已订阅的计划交易信息
在User-Agent header 配置 APIKey

header: {"Authorization" : "Bearer YourAPIKey"}

id_list 请求例子:

123;456;e3145e8-0648-11e8-934e-00163e00
1654;354;687
a7c31ec4-df10-11e8-ad3c-0a580a31034a;c4c9e32a-7343-11e7-a8d0-00163a004d3f
API 返回码
API 返回的结果是 JSON 格式, 示例如下:


  {
      "info": "",
      "statusCode": 200,
      "message": "请求成功",
      "data": [
          {
              "strategy_name": "xxxxxxx",
              "last_run_date": "xxxxxxx",
              "notebook_id": "xxxxxxxxxxxxxxxx",
              "id": 1234,
              "planned_orders": []
          }
      ],
      "result": true,
      "metadata": {
          "total_count": 3
      }
  }
  {
      "message": "请求失败",
      "result": false,
      "info": {
          "FailureReason": "没有结果返回，请确认策略id，或策略运行状态"
      },
      "statusCode": 4004
  }
  {
      "info": {
          "FailureReason": "Account Validation Failed"
      },
      "statusCode": 4002,
      "result": false,
      "message": "请求失败"
  }
  {
      "message": "请求失败",
      "result": false,
      "info": {
          "FailureReason": "POST Missing key"
      },
      "statusCode": 4001
  }
  {
      "info": {
          "FailureReason": "Only Accept POST"
      },
      "statusCode": 4003,
      "result": false,
      "message": "请求失败"
  }
      
result: API 请求是否成功

statusCode: API 返回码

message: API 返回码的中文解释

Data: 数据信息

info: 具体原因

API 返回码如下:

API 返回码	含义
200	请求成功
4001	key不能为空
4002	账户未激活或认证失败
4003	请求方法错误
4004	没有结果返回，请确认策略id，或策略运行状态
500	服务器错误
