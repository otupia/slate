---
title: API Reference

language_tabs:
  - python

toc_footers:
  - <a href='mailto:caojianpu@ucfgroup.com'>邮件</a>

includes:
  - errors

search: true
---

# 介绍

    第一甩单接口列表

    <aside class="warning">
        <b>今日IP： 10.20.83.42</b>
    </aside>


# 注册登录相关接口

## 发送验证码接口

```python
    # coding=utf-8
    import httplib, urllib

    httpClient = None
    try:

        httpClient = httplib.HTTPConnection("<IP>", 8080, timeout=30)
        httpClient.request("GET", "/checkmessage?key=1&format=json&sign=1111111111", "")
        response = httpClient.getresponse()
        print response.read()
    except Exception, e:
        print e
    finally:
        if httpClient:
            httpClient.close()

```
> 验证码发送成功

```json
    {
        "success": true
    }
```

> 验证码发送失败

```json
    {
        "success": false,
        "errorMessage": "send message failed"
    }
```


向指定手机号发送验证码短信，并以入参 key 为标识存入session。


### http 地址
`GET http://<IP>:8080/checkmessage?key=1&format=json&sign=1111111111`

### 参数说明
参数名称 | 是否必须 | 说明 | 示例
--------- | ------- | ------- | -----------
key | Y | 存入session的关键字 |"regist_18622158558"
format | Y | 返回格式，现阶段请使用json | "json"
sign | Y | 签名 | "1111111111"

<aside class="warning">现阶段签名未校验</aside>

## 提交注册信息

```python
import httplib, urllib
httpClient = None

try:
    params = urllib.urlencode({
        'securityCode' : '188719',
        'telephone' : '1111111111111',
        'password' : '123456',
        'confirmPassword' : '123456',
        'format' : 'json',
        'sign' : '123456',
        })
    headers = {"Content-type": "application/x-www-form-urlencoded"
                    , "Accept": "application/json"}
    httpClient = httplib.HTTPConnection(IP, 8080, timeout=30)
    httpClient.request("POST", "/register", params, headers)
    response = httpClient.getresponse()
    print response.read()
except Exception, e:
    print e
finally:
    if httpClient:
        httpClient.close()
```
> 注册成功

```json
    {
        "sucessed": true,
        "message": "LoanOfficeUser exist, allows to Login"
    }
```

> 注册失败

```json
    {
        "sucessed": false,
        "errorMessage": "captcha is not avalible."
    }
```


提交信贷员注册信息

### http 地址
`POST http://<IP>:8080/register`

### 参数说明
参数名称 | 是否必须 | 说明 | 示例
--------- | ------- | ------- | -----------
securityCode | Y | 验证码，为六位随机数字，必须与session中 "regist_<telephone>" 对应值记录的一致 |"123456"
telephone | Y | 电话号码 |"1864567890"
password | Y | 密码 |"123456"
confirmPassword | Y | 确认密码 | "123456"
format | Y | 返回格式，现阶段请使用json | "json"
sign | Y | 签名 | "1111111111"

<aside class="warning">
注意：
<ul>
    <li>现阶段签名未校验</li>
    <li>在短信不能发送阶段,可以访问 http://10.20.83.42:8080/session?key=KEY 获得session内的值</li>
</ul>
</aside>

## 用户登录验证

```python
import httplib, urllib
httpClient = None

try:
    params = urllib.urlencode({
        'telephone' : '1111111111111',
        'password' : '123456',
        'format' : 'json',
        'sign' : '123456',
        })
    headers = {"Content-type": "application/x-www-form-urlencoded"
                    , "Accept": "application/json"}
    httpClient = httplib.HTTPConnection(IP, 8080, timeout=30)
    httpClient.request("POST", "/login", params, headers)
    response = httpClient.getresponse()
    print response.read()
except Exception, e:
    print e
finally:
    if httpClient:
        httpClient.close()
```
> 登录成功

```json
    {
        "sucessed": true,
        "message": "LoanOfficeUser exist, allows to Login",

    }
```

> 登录失败

```json
    {
        "sucessed": false,
        "errorMessage": ""
    }
```


提交信贷员注册信息

### http 地址
`POST http://<IP>:8080/register`

### 参数说明
参数名称 | 是否必须 | 说明 | 示例
--------- | ------- | ------- | -----------
securityCode | Y | 验证码，为六位随机数字，必须与session中 "regist_<telephone>" 对应值记录的一致 |"123456"
telephone | Y | 电话号码 |"1864567890"
password | Y | 密码 |"123456"
confirmPassword | Y | 确认密码 | "123456"
format | Y | 返回格式，现阶段请使用json | "json"
sign | Y | 签名 | "1111111111"

<aside class="warning">
注意：
<ul>
    <li>现阶段签名未校验</li>
    <li>在短信不能发送阶段,可以访问 http://10.20.83.42:8080/session?key=KEY 获得session内的值</li>
</ul>
</aside>
# 甩单相关接口
## 提交甩单信息

```python
import httplib, urllib
httpClient = None

try:
    params = urllib.urlencode({
        #。。。 。。。
        })
    headers = {"Content-type": "application/x-www-form-urlencoded"
                    , "Accept": "application/json"}
    httpClient = httplib.HTTPConnection(IP, 8080, timeout=30)
    httpClient.request("POST", "/login", params, headers)
    response = httpClient.getresponse()
    print response.read()
except Exception, e:
    print e
finally:
    if httpClient:
        httpClient.close()
```
> 甩单成功

```json
    {
        "sucessed": true

    }
```

> 登录失败

```json
    {
        "sucessed": false,
        "errorMessage": ""
    }
```


提交信贷员注册信息

### http 地址
`POST http://<IP>:8080/loanrequest/`

### 参数说明
参数名称 | 是否必须 | 说明 | 示例
--------- | ------- | ------- | -----------
request_amount | Y | 请求贷款金额 |100.0
customerType  | Y | 用户类型 1: 上班族;2: 企业;| 2
loan_type | Y | 贷款类型 1: 信用贷;2: 车贷;3: 房贷; | 2
loan_term | Y | 1: 3个月内;2: 6个月;3: 1年;4: 2年;5: 3年;6: 4年;7: 5年及以上; | 2
customer_info.name  | Y | 用户姓名 | aliang
customer_info.sex | Y | 用户性别 1: 男;2: 女; | 1
customer_info.id_no  | Y | 身份证号 |120106199902259999
customer_info.telephone | N | 用户手机号| 18622158296
customer_info.company_type | N | 公司类型 1: 国企/事业单位;2: 500强企业;3: 上市公司;4: 民营企业;| 2
customer_info.house_hold | N | 户口类型 | 京户
customer_info.income | N | 月收入 | 600.0
customer_info.income_pay_type | N | 工资类型 1: 打卡;2: 网银转账;3: 现金;4: 其他; | 2
customer_info.have_secure | N | 是否有保险 1: 是;2: 否; | 1
customer_info.have_house_fund | N | 是否有公积金 1: 是;2: 否; | 1
customer_info.debit_card_limit | N | 信用卡限额 | 10000.0
customer_info.loaned_amount | Y | 已贷款金额 | 100000.0
customer_info.have_house | N | 是否有房子 1: 是;2: 否; | 1
customer_info.house_location | N | 房屋所在地 | 北京
customer_info.house_amount | N | 房屋数量 | 2
customer_info.house_type | N | 房屋类型 1: 商品住宅;2: 商住两用;3: 商铺;4: 办公楼;5: 经适/限价房;6: 房改/危改房;7: 小产权房;8: 宅基地/自建房; | 2
customer_info.house_status | N | 房屋状态 1: 全款;2: 按揭;3: 已抵押;4: 已质押; | 2
customer_info.house_loan | N | 是否有房贷 1: 是;2: 否; | 2
customer_info.have_house_cert | N | 是否有房本 1: 是;2: 否; | 1
customer_info.accept_house_mortgage | N | 是否接受房贷 1: 是;2: 否;  | 1
customer_info.have_car | N | 是否有车  1: 是;2: 否; | 2
customer_info.car_licence | N | 车牌号 | 京Q123456
customer_info.car_amount | N | 车数量 | 2
customer_info.accept_car_mortgage | N | 是否接受车贷 1: 是;2: 否; | 1
customer_info.loaned_from_company | N | 已贷款公司 | 宜人贷;人人贷;
customer_info.remark | N | 备注 | 长得不错
format | Y | 现阶段请使用json | "json"
sign | Y | 签名 | "1111111111"

<aside class="warning">
注意：
<ul>
    <li>现阶段签名未校验</li>
    <li>注意使用 POST 方式 </li>
</ul>
</aside>
