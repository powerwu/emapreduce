# AddClusterService {#concept_ss5_1w2_2gb .concept}

为指定的集群添加当前集群的主版本支持的某项服务。

## 请求参数 {#section_p5v_ffb_kfb .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ClusterId|String|是|C-D7958B72E59BAB88|集群 ID|
|RegionId|String|是|cn-hangzhou|区域 ID|
|AccessKeyId|String|否|LTAI8ljWyu7y\*\*\*\*|AccessKeyId|
|Comment|String|否|addService|本次添加服务的备注信息|
|Service.N.ServiceName|String|否|HDFS|待添加的服务名称，例如 HDFS、YARN|

## 返回参数 {#section_vdw_lv4_dgb .section}

|字段|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|EBB4D49C-4064-4818-B3AE-4C6BE5FC8264|请求 ID|

## 示例 {#section_ydw_lv4_dgb .section}

-   请求示例

    ```
    /?ClusterId=C-F32FB31D82954C64
    &RegionId=cn-hangzhou
    &AccessKeyId=LTAI8ljWyu7y****
    &Comment=addService
    &Service.1.ServiceName=HDFS
    &<公共请求参数>
    ```

-   正常返回示例

    JSON 格式

    ```
    {
    	"requestId":"EBB4D49C-4064-4818-B3AE-4C6BE5FC8264"
    }
    ```

-   异常返回示例

    JSON 格式

    ```
    {
    	"code":"RAM.Permission.NotAllow",
    	"message":"It is not allow to execute this operation,please use RAM to authorize!",
    	"requestId":"9AEDC439-1F63-491D-B8C6-9737C372BF3A",
    	"successResponse":false
    }
    ```


## 错误码 {#section_a2w_lv4_dgb .section}

[查看本产品错误码](https://error-center.alibabacloud.com/status/product/Emr)

