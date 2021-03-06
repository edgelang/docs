# staking
# 目录
1. [交易](#交易)
2. [查询](#查询)
## 交易
| **命令**                   | **解释**                                  |
| -------------------------- | ---------------------------------------- |
| [create-validator](#create-validator)  | 创建一个新的验证者              |
| [edit-validator](#edit-validator)      | 编辑一个存在的验证者            |
| [delegate](#delegate)                  | 委托bhp到验证者                |
| [redelegate](#redelegate)              | 转移委托从一个验证者到另一个验证者 |
| [unbound](#unblund)                    | 取消委托                       |


### create-validator
#### 解释：在已有网络上创建一个新的验证者。
```bash
--amount 自委托的数量
--pukey 节点公钥
--moniker 验证者名字
--details 验证者详细信息
--commission-rate 验证者佣金比例
--commission-max-rate 验证者最大佣金比例
--commission-max-change-rate 验证者修改佣金比例时最大改变量比例
--min-self-delegation 最少委托的数量
```
#### 完整演示命令如下：
```bash
bhpcli tx staking create-validator \
--amount=2000000000000abhp \
--pubkey=$(bhpd tendermint show-validator) \
--moniker="DemoValidator" \
--details="I'm a good validator" \
--commission-rate="0.10" \
--commission-max-rate="0.20" \
--commission-max-change-rate="0.01" \
--min-self-delegation="1" \
--from=demokey \
--chain-id=testing \
--gas=auto \
--gas-prices="2.5abhp" \
--gas-adjustment=2
```
#### 输出
```json
{
    "height": "0",
    "txhash": "2BCC8258B013775CE95EA11A92065D663DE2E02514446BAB1E4B56E426B59ECA",
    "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"create_validator\"}]}]}]",
    "logs": [
        {
            "msg_index": 0,
            "success": true,
            "log": "",
            "events": [
                {
                    "type": "message",
                    "attributes": [
                        {
                            "key": "action",
                            "value": "create_validator"
                        }
                    ]
                }
            ]
        }
    ]
}
```
### edit-validator
#### 解释：可以编辑验证人信息，如网站，不修改的信息，保持创建时的值。
```bash
--website 设置网址
--identity 设置 https://keybase.io 上用户的头像
```
#### 完整演示命令如下：
```bash
bhpcli tx staking edit-validator \
--website "https://bhpa.io" \
--from demokey \
--chain-id "testing" \
--gas=auto \
--gas-prices="2.5abhp" \
--gas-adjustment=2
```
#### 输出：
```json
{
  "height": "0",
  "txhash": "AECE9FD1049493258304349084943965A65708DCEDC6533D9904C1F7F52BA700",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"edit_validator\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "edit_validator"
            }
          ]
        }
      ]
    }
  ]
}
```
### delegate
#### 解释：委托BHP到验证者
#### 完整演示命令如下：其中bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y为验证者地址
```bash
bhpcli tx staking delegate \
bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y \
10000000000abhp \
--from key1 \
--chain-id testing \
--gas=auto \
--gas-prices="2.5abhp" \
--gas-adjustment=2
```
#### 输出：
```json
{
  "height": "0",
  "txhash": "B08AF07ECB8DEC39B9DC02C3C36C5B86925E81B4672721B3440F63145CE3E6A5",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"delegate\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "delegate"
            }
          ]
        }
      ]
    }
  ]
}
```
### redelegate
#### 解释：转移委托从一个验证者到另一个验证者
#### 演示命令如下：其中bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y为原验证者地址，bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs为新验证者地址。
```bash
bhpcli tx staking redelegate \
bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y \
bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs \
10000000000abhp \
--from key1 \
--chain-id testing \
--gas=auto \
--gas-prices="2.5abhp" \
--gas-adjustment=2
```
#### 输出：
```json
{
  "height": "0",
  "txhash": "48D0A12CE5A52B4865A99D5160095B879234668DE2605442C0C9A6F043EA066F",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"begin_redelegate\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "begin_redelegate"
            }
          ]
        }
      ]
    }
  ]
}
```
### unbound
#### 解释：从验证者取消委托，默认解除周期是2周
#### 演示命令如下：其中bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y是验证者地址
```bash
bhpcli tx staking unbond \
bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y \
5000000000abhp \
--from key1 \
--chain-id testing \
--gas=auto \
--gas-prices="2.5abhp" \
--gas-adjustment=2
```
#### 输出
```json
{
  "height": "0",
  "txhash": "EE03F06F1E960969F421600D3DDFD10FCCC19D68D030E04D156D868155F115C9",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"begin_unbonding\"}]}]}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "action",
              "value": "begin_unbonding"
            }
          ]
        }
      ]
    }
  ]
}

```
## 查询
| **命令**                    | **解释**                                                    |
| -------------------------- | ----------------------------------------------------------- |
| [delegation](#delegation)  | 查询委托者在一个特定验证者上的委托                  |
|[delegations](#delegations)                | 查询一个委托者的所有委托记录                                |
| [unbonding-delegation](#unbonding-delegation)       | 使用委托者地址查询一个验证者上所有解除委托的记录         |
| [unbonding-delegations](#unbonding-delegations)      | 使用委托者地址查询所有取消委托的记录                        |
| [redelegation](#redelegation)               | 使用委托者地址和前、后验证者地址查询重新委托记录     |
| [redelegations](#redelegations)              | 使用委托者地址查询所有转委托的记录                        |
| [validator](#validator)                  | 查询一个验证者的信息                                     |
| [validators](#validators)                 | 查询网络上所有验证者的信息                               |
| [delegations-to](#delegations-to)             | 查询一个验证者上的所有委托记录                           |
| [unbonding-delegations-from](#unbonding-delegations-from) | 查询一个验证者上的所有解除委托记录                       |
| [redelegations-from](#redelegations-from)         | 查询从这个验证者转移的委托记录  |
| [params](#params)                     | 查询当前staking的参数，如                                   |
| [pool](#pool)                       | 查询staking池中委托的未委托的token数量                   |

### delegation
解释：查询用户在一个特定验证者上的委托bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y为验证者地址
演示命令：
```bash
bhpcli query staking delegation \
$(bhpcli keys show key1 -a) \ bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y
```
输出：
```json
{
  "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
  "validator_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
  "shares": "10000000000.000000000000000000",
  "balance": "10000000000"
}
```
### delegations
#### 解释:查询一个委托者的所有委托
#### 演示命令
```bash
bhpcli query staking delegations $(bhpcli keys show key1 -a)
```
#### 输出
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_address": "bhpvaloper1ceccntfep63j7fwrzapk9w0zvw900s392xsc2c",
    "shares": "10000000000.000000000000000000",
    "balance": "9900000000"
  },
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "shares": "5000000000.000000000000000000",
    "balance": "5000000000"
  }
]
```

### unbonding-delegation
#### 解释：使用委托者地址查询一个验证者上所有解除委托的记录
#### 演示命令
```bash
bhpcli query staking unbonding-delegation \
 $(bhpcli keys show key1 -a) \
 bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs
```
#### 输出
```json
{
  "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
  "validator_address": "bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
  "entries": [
    {
      "creation_height": "75288",
      "completion_time": "2020-09-02T12:14:01.219526635Z",
      "initial_balance": "10000000000",
      "balance": "10000000000"
    }
  ]
}
```
### unbonding-delegations
#### 解释：查询委托者的所有正在解除委托的记录
#### 演示命令
```bash
 bhpcli query staking unbonding-delegations $(bhpcli keys show key1 -a)
```
#### 输出
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_address": "bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
    "entries": [
      {
        "creation_height": "75288",
        "completion_time": "2020-09-02T12:14:01.219526635Z",
        "initial_balance": "10000000000",
        "balance": "10000000000"
      }
    ]
  },
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "entries": [
      {
        "creation_height": "78539",
        "completion_time": "2020-09-03T02:03:43.939593147Z",
        "initial_balance": "5000000000",
        "balance": "5000000000"
      }
    ]
  }
]
```
### redelegation
#### 解释：使用委托者地址和前、后验证者地址查询重新委托记录,其中bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y为先前委托者地址，
bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs为转移到的委托者地址
#### 演示命令
```bash
bhpcli query staking redelegation \
$(bhpcli keys show key1 -a) \
bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y \
bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs
```
#### 输出
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_src_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "validator_dst_address": "bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
    "entries": [
      {
        "creation_height": 75266,
        "completion_time": "2020-09-02T12:08:24.349376004Z",
        "initial_balance": "10000000000",
        "shares_dst": "10000000000.000000000000000000",
        "balance": "10000000000"
      }
    ]
  }
]
```
### redelegations
#### 解释:使用委托者地址查询所有转委托的记录
#### 演示命令：
```bash
bhpcli query staking redelegations $(bhpcli keys show key1 -a)
```
#### 输出：
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_src_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "validator_dst_address": "bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
    "entries": [
      {
        "creation_height": 75266,
        "completion_time": "2020-09-02T12:08:24.349376004Z",
        "initial_balance": "10000000000",
        "shares_dst": "10000000000.000000000000000000",
        "balance": "10000000000"
      }
    ]
  }
]
```
### validator
#### 解释：查询一个给定地址的验证者信息
#### 演示命令：
```bash
bhpcli query staking validator \
bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs
```
#### 输出：
```json
{
  "operator_address": "bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
  "consensus_pubkey": "bhpvalconspub1zcjduepq64suxf6rrklnxu6e7jysqenv73k55ynqttr6s4q50aptsr7phtms9nexjs",
  "jailed": false,
  "status": 2,
  "tokens": "200000000000000",
  "delegator_shares": "200000000000000.000000000000000000",
  "description": {
    "moniker": "node1",
    "identity": "",
    "website": "",
    "details": ""
  },
  "unbonding_height": "0",
  "unbonding_time": "1970-01-01T00:00:00Z",
  "commission": {
    "commission_rates": {
      "rate": "0.000000000000000000",
      "max_rate": "0.000000000000000000",
      "max_change_rate": "0.000000000000000000"
    },
    "update_time": "2020-08-06T03:54:28.120981631Z"
  },
  "min_self_delegation": "1"
}
```
### validators
#### 解释：查询网络上所有验证者信息
#### 演示命令：
```bash
bhpcli query staking validators
```
#### 输出：
```json
[
    {
        "operator_address":"bhpvaloper1rr0u7tgaz07y670tpfqma7p8nmscpk6wcghkfr",
        "consensus_pubkey":"bhpvalconspub1zcjduepqfzfrw48rzzvq5hrhcrk0g92s6cu3scmm0d7d88hx79xv8x75l78squd0p5",
        "jailed":false,
        "status":2,
        "tokens":"100000000000",
        "delegator_shares":"100000000000.000000000000000000",
        "description":{
            "moniker":"testing",
            "identity":"",
            "website":"",
            "details":"yes I'm a good validator"
        },
        "unbonding_height":"74506",
        "unbonding_time":"2020-09-02T08:54:26.424051297Z",
        "commission":{
            "commission_rates":{
                "rate":"0.100000000000000000",
                "max_rate":"0.200000000000000000",
                "max_change_rate":"0.010000000000000000"
            },
            "update_time":"2020-08-19T06:31:31.050995911Z"
        },
        "min_self_delegation":"1"
    },
    {
        "operator_address":"bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
        "consensus_pubkey":"bhpvalconspub1zcjduepq64suxf6rrklnxu6e7jysqenv73k55ynqttr6s4q50aptsr7phtms9nexjs",
        "jailed":false,
        "status":2,
        "tokens":"200000000000000",
        "delegator_shares":"200000000000000.000000000000000000",
        "description":{
            "moniker":"node1",
            "identity":"",
            "website":"",
            "details":""
        },
        "unbonding_height":"0",
        "unbonding_time":"1970-01-01T00:00:00Z",
        "commission":{
            "commission_rates":{
                "rate":"0.000000000000000000",
                "max_rate":"0.000000000000000000",
                "max_change_rate":"0.000000000000000000"
            },
            "update_time":"2020-08-06T03:54:28.120981631Z"
        },
        "min_self_delegation":"1"
    },
    {
        "operator_address":"bhpvaloper10y9fd3m2zkz5jk58matygpy7wjjtacgg7uc5u7",
        "consensus_pubkey":"bhpvalconspub1zcjduepqwgpq9zemyvter67tltdg8a78ckwzkgxfpl3njz3fe6kk8dpgumessnt7mt",
        "jailed":false,
        "status":2,
        "tokens":"200000000000000",
        "delegator_shares":"200000000000000.000000000000000000",
        "description":{
            "moniker":"node3",
            "identity":"",
            "website":"",
            "details":""
        },
        "unbonding_height":"0",
        "unbonding_time":"1970-01-01T00:00:00Z",
        "commission":{
            "commission_rates":{
                "rate":"0.000000000000000000",
                "max_rate":"0.000000000000000000",
                "max_change_rate":"0.000000000000000000"
            },
            "update_time":"2020-08-06T03:54:28.120981631Z"
        },
        "min_self_delegation":"1"
    },
    {
        "operator_address":"bhpvaloper10au77t30anhmgrvnc8dxtl7lzjq76f58ms3kqw",
        "consensus_pubkey":"bhpvalconspub1zcjduepqsxwspe6h27k7fkk85xg46rzmg2jeksxuw6ry3jkyf7m8r38puyjq3asqef",
        "jailed":false,
        "status":2,
        "tokens":"200001000000000",
        "delegator_shares":"200001000000000.000000000000000000",
        "description":{
            "moniker":"node2",
            "identity":"",
            "website":"",
            "details":""
        },
        "unbonding_height":"0",
        "unbonding_time":"1970-01-01T00:00:00Z",
        "commission":{
            "commission_rates":{
                "rate":"0.000000000000000000",
                "max_rate":"0.000000000000000000",
                "max_change_rate":"0.000000000000000000"
            },
            "update_time":"2020-08-06T03:54:28.120981631Z"
        },
        "min_self_delegation":"1"
    },
    {
        "operator_address":"bhpvaloper1ceccntfep63j7fwrzapk9w0zvw900s392xsc2c",
        "consensus_pubkey":"bhpvalconspub1zcjduepqk6h5fps87hyqhs9xn5w4pt9trlj56z4l9dy5ww77tee508fzzplq99lqam",
        "jailed":true,
        "status":1,
        "tokens":"9900000000",
        "delegator_shares":"10000000000.000000000000000000",
        "description":{
            "moniker":"DemoValidator",
            "identity":"",
            "website":"",
            "details":"I'm a good validator"
        },
        "unbonding_height":"75398",
        "unbonding_time":"2020-09-02T12:42:05.596015117Z",
        "commission":{
            "commission_rates":{
                "rate":"0.100000000000000000",
                "max_rate":"0.200000000000000000",
                "max_change_rate":"0.010000000000000000"
            },
            "update_time":"2020-08-19T11:45:56.912423355Z"
        },
        "min_self_delegation":"1"
    },
    {
        "operator_address":"bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
        "consensus_pubkey":"bhpvalconspub1zcjduepq6v05ucccwfv74d5en3lfnqya9zw6xwn50wml8rlge0kfpxk0jhksmnv7pa",
        "jailed":false,
        "status":2,
        "tokens":"200005000000000",
        "delegator_shares":"200005000000000.000000000000000000",
        "description":{
            "moniker":"node0",
            "identity":"",
            "website":"",
            "details":""
        },
        "unbonding_height":"0",
        "unbonding_time":"1970-01-01T00:00:00Z",
        "commission":{
            "commission_rates":{
                "rate":"0.000000000000000000",
                "max_rate":"0.000000000000000000",
                "max_change_rate":"0.000000000000000000"
            },
            "update_time":"2020-08-06T03:54:28.120981631Z"
        },
        "min_self_delegation":"1"
    },
    {
        "operator_address":"bhpvaloper17d3trevfrw9mu6zv9g8txzk83ec8gc4czsgswu",
        "consensus_pubkey":"bhpvalconspub1zcjduepqvqnwel8ej55rtugypjwv0elf7zed489a2d6mdfa7ejxemwpx4ahsty3e30",
        "jailed":true,
        "status":1,
        "tokens":"99000000000",
        "delegator_shares":"100000000000.000000000000000000",
        "description":{
            "moniker":"DemoValidator",
            "identity":"",
            "website":"https://bhpa.io",
            "details":"I'm a good validator"
        },
        "unbonding_height":"75225",
        "unbonding_time":"2020-09-02T11:57:56.564863935Z",
        "commission":{
            "commission_rates":{
                "rate":"0.100000000000000000",
                "max_rate":"0.200000000000000000",
                "max_change_rate":"0.010000000000000000"
            },
            "update_time":"2020-08-19T11:32:09.686819326Z"
        },
        "min_self_delegation":"1"
    }
]
```
### delegations-to
#### 解释：查询一个验证者上的所有委托记录
#### 演示命令：
```bash
bhpcli query staking delegations-to bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y
```
#### 输出：
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "shares": "5000000000.000000000000000000",
    "balance": "5000000000"
  },
  {
    "delegator_address": "bhp1eesqv2r4v2al6dn5wavndm96fwth3y6s7dd87y",
    "validator_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "shares": "200000000000000.000000000000000000",
    "balance": "200000000000000"
  }
]
```
### unbonding-delegations-from
#### 解释：查询一个验证者上的所有解除委托记录 
#### 演示命令：
```bash
bhpcli query staking unbonding-delegations-from bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y
```
#### 输出：
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "entries": [
      {
        "creation_height": "78539",
        "completion_time": "2020-09-03T02:03:43.939593147Z",
        "initial_balance": "5000000000",
        "balance": "5000000000"
      }
    ]
  }
]

```
### redelegations-from
#### 解释：查询从这个验证者转移的委托记录
#### 演示命令：
```bash
 bhpcli query staking redelegations-from bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y 
```
#### 输出：
```json
[
  {
    "delegator_address": "bhp1ceccntfep63j7fwrzapk9w0zvw900s39q95z9c",
    "validator_src_address": "bhpvaloper1eesqv2r4v2al6dn5wavndm96fwth3y6s5wfa3y",
    "validator_dst_address": "bhpvaloper1t7gmv3qraqc7urcp2jqk2wv54p9jrevn0546cs",
    "entries": [
      {
        "creation_height": 75266,
        "completion_time": "2020-09-02T12:08:24.349376004Z",
        "initial_balance": "10000000000",
        "shares_dst": "10000000000.000000000000000000",
        "balance": "10000000000"
      }
    ]
  }
]
```
### params
#### 解释：查询当前staking的参数
#### 演示命令：
```bash
bhpcli query staking params
```
#### 输出：
```json
{
  "unbonding_time": "1209600000000000",
  "max_validators": 21,
  "max_entries": 7,
  "bond_denom": "abhp"
}
```
### pool
#### 解释：查询staking池中委托的未委托的bhp数量
#### 演示命令：
```bash
bhpcli query staking pool
```
#### 输出：
```json
{
  "not_bonded_tokens": "133900000000",
  "bonded_tokens": "800106000000000"
}
```
