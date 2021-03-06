# ListFlowCluster {#concept_myd_mk2_ggb .concept}

调用 ListFlowCluster 接口查询项目中可用的集群列表

## 请求参数 {#section_obj_yxl_2gb .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ProjectId|String|是|FP-5D55DA9DEDF22ED3|项目ID|
|PageNumber|Integer|否|1|页码|
|RegionId|String|是|cn-hangzhou|区域 ID|
|PageSize|Integer|否|20|每页查询数量|

## 返回参数 {#section_vbj_yxl_2gb .section}

|字段|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0d18b019-00ab-455f-b60c-2891bf02f538|请求 ID|
|TotalCount|Integer|42|总数|
|PageNumber|Integer|1|页码|
|PageSize|Integer|20|每页数量|
|Clusters| | |集群列表|
|Id|String|C-2E6ABBD39BD09F97|集群 ID|
|Name|String|String|集群名字|
|Type|String|HADOOP|类型|
|CreateTime|Long|1542953603000|创建时间|
|RunningTime|Integer|200|运行时间，单位：秒|
|Description|String|my flow demo|工作流描述|
|Status|String|SUCCESS|状态|
|ChargeType|String|PostPaid|收费方式|
|ExpiredTime|Long|1542953603000|过期时间|
|Period|Integer|1|周期|
|HasUncompletedOrder|Boolean|false|是否有未完成订单|
|OrderList|String|1,2|订单列表|
|CreateResource|String|ECM\_EMR|资源|
|OrderTaskInfo| | |订单任务信息|
|TargetCount|Integer|2|目标数量|
|CurrentCount|Integer|2|当前数量|
|OrderIdList|String|1,2|订单列表|
|FailReason| | |集群失败原因|
|ErrorCode|String|123|错误码|
|ErrorMsg|String|failed|错误原因|
|RequestId|String|0d18b019-00ab-455f-b60c-2891bf02f538|请求 ID|

## 示例 {#section_dcj_yxl_2gb .section}

-   请求示例

    ```
    
    /?ProjectId=FP-5D55DA9DEDF22ED3
    &RegionId=cn-hangzhou
    &PageNumber=1
    &PageSize=20
    &<公共请求参数>
    ```

-   正常返回示例

    JSON 格式

    ```
    {
    	"Clusters":{
    		"ClusterInfo":[
    			{
    				"ChargeType":"PostPaid",
    				"CreateResource":"ECM_EMR",
    				"CreateTime":1542953603000,
    				"FailReason":{},
    				"HasUncompletedOrder":false,
    				"Id":"C-4042079DFF01A3F5",
    				"Name":"zx-presto-1",
    				"OrderTaskInfo":{},
    				"RunningTime":1322,
    				"Status":"IDLE",
    				"Type":"HADOOP"
    			},
    			{
    				"ChargeType":"PostPaid",
    				"CreateResource":"ECM_EMR",
    				"CreateTime":1542950611000,
    				"FailReason":{},
    				"HasUncompletedOrder":false,
    				"Id":"C-3D0B53253595DBB0",
    				"Name":"zx-presto-213",
    				"OrderTaskInfo":{},
    				"RunningTime":4314,
    				"Status":"IDLE",
    				"Type":"HADOOP"
    			}
    		]
    	},
    	"PageNumber":1,
    	"PageSize":10,
    	"TotalCount":2
    }
    ```

-   异常返回示例

    JSON 格式

    ```
    {
    	"Clusters":{
    		"ClusterInfo":[
    			{
    				"ChargeType":"PostPaid",
    				"CreateResource":"ECM_EMR",
    				"CreateTime":1542953603000,
    				"FailReason":{},
    				"HasUncompletedOrder":false,
    				"Id":"C-4042079DFF01A3F5",
    				"Name":"zx-presto-1",
    				"OrderTaskInfo":{},
    				"RunningTime":1322,
    				"Status":"IDLE",
    				"Type":"HADOOP"
    			},
    			{
    				"ChargeType":"PostPaid",
    				"CreateResource":"ECM_EMR",
    				"CreateTime":1542950611000,
    				"FailReason":{},
    				"HasUncompletedOrder":false,
    				"Id":"C-3D0B53253595DBB0",
    				"Name":"zx-presto-213",
    				"OrderTaskInfo":{},
    				"RunningTime":4314,
    				"Status":"IDLE",
    				"Type":"HADOOP"
    			}
    		]
    	},
    	"PageNumber":1,
    	"PageSize":10,
    	"TotalCount":2
    }
    ```


## 错误码 {#section_fcj_yxl_2gb .section}

[查看本产品错误码](https://error-center.alibabacloud.com/status/product/Emr)

