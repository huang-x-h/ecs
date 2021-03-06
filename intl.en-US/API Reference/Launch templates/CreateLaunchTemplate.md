# CreateLaunchTemplate {#CreateLaunchTemplate .reference}

Creates an instance launch template, or launch template for short. An instance launch template saves you the trouble of entering a large number of configuration parameters each time you create an instance.

## Description {#section_whw_2sn_12b .section}

Instance launch templates contain configurations used to create instances, such as the instance region, image ID, instance type, security group ID, and internet bandwidth settings. If you do not specify a certain instance configuration in the template, you must specify this configuration when creating an instance. When creating templates \(CreateLaunchTemplate\), the template version numbers start from 1. After creating one template, you can create multiple versions based on this template \(CreateLaunchTemplateVersion\). Version numbers start from 1 and increase sequentially. If you do not specify a template version number when creating an instance \([RunInstances](reseller.en-US/API Reference/Instances/RunInstances.md#)\), default version is used.

When you call this interface, consider the following:

-   You can create up to 30 instance launch templates per region. Each template can have up to 30 versions.

-   Most instance launch template parameters are optional. When you create a template, ECS does not verify the existence or validity of its parameter values. The validity of parameter values is only verified when you create instances.

-   If you set a certain configuration in an instance launch template, you cannot filter out this configuration when creating an instance \([RunInstances](reseller.en-US/API Reference/Instances/RunInstances.md#)\). For example, if you set `HostName=LocalHost` in the template and in RunInstances the value of `HostName` is null, the `LocalHost` still takes effect. If you want to overwrite the `HostName=LocalHost` configuration, set `HostName=MyHost` in RunInstances or other parameter values if you want.


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: CreateLaunchTemplate.|
|RegionId|String|Yes|Region ID of an instance. For more information, call [DescribeRegions](../reseller.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|LaunchTemplateName|String|Yes|Instance launch template name. Can contain \[2, 128\] characters in length. It must start with an English letter \(uppercase or lowercase\) and can contain numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It cannot start with "http://" or "https://".|
|VersionDescription|String|No|Description of instance launch template version 1. It can be \[2, 256\] characters in length. It cannot start with "http://" or "https://". The default value is null.|
|ImageId|String|No|Image ID.|
|InstanceType|String|No|Instance type. For more information, call [DescribeInstanceTypes](reseller.en-US/API Reference/Instances/DescribeInstanceTypes.md#) to obtain the latest instance type list.|
|SecurityGroupId|String|No|The security group ID.|
|NetworkType|String|No|Network type of the instance. Value options: Classic | VPC.|
|VSwitchId|String|No|When creating a VPC-Connected instance, you must specify its VSwitch ID.|
|InstanceName|String|No|The name of the instance. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|Description|String|No|Instance description.|
|InternetMaxBandwidthIn|String|No|The maximum inbound bandwidth from the internet network, measured in Mbit/s. Value range: \[1, 200\].|
|InternetMaxBandwidthOut|String|No|Maximum outbound bandwidth from the Internet, its unit of measurement is Mbit/s. Value range: \[0, 100\].|
|HostName|String|No|Instance host name.-   It cannot start or end with a period \(.\) or a hyphen \(-\) and it cannot have two or more consecutive periods \(.\) or hyphens \(-\).
-   For Windows: The host name can be \[2, 15\] characters in length. It can contain A-Z, a-z, numbers, periods \(.\), and hyphens \(-\). It cannot only contain numbers.
-   For other operating systems: The host name can be \[2, 64\] characters in length. It can be segments separated by periods \(.\). It can contain A-Z, a-z, numbers, and hyphens \(-\).

|
|ZoneId|String|No|The zone ID of the instance.|
|SystemDisk.Category|String|No|The category of the system disk. System disk type. Optional values:-   Cloud: Basic cloud disk.
-   cloud\_efficiency: Ultra cloud disk.
-   cloud\_ssd: SSD Cloud Disks.
-   ephemeral\_ssd: Ephemeral SSD.

|
|SystemDisk.Size|Integer|No|Size of the system disk, measured in GB. Value range: \[20, 500\].|
|SystemDisk.DiskName|String|No|System disk name. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|SystemDisk.Description|String|No|System disk description. It cannot begin with http:// or https://.|
|DataDisk.n.Category|String|No|The data disk type. Value range of `n`: \[1, 16\]. Optional values-   Cloud: Basic cloud disk.
-   cloud\_efficiency: Ultra cloud disk.
-   cloud\_ssd: SSD Cloud Disks.
-   ephemeral\_ssd: Ephemeral SSD.

|
|DataDisk.n.Size|Integer|No|The data disk capacity. Value range of `n`: \[1, 16\]. Value range:-   cloud: \[5, 2000\]
-   cloud\_efficiency: \[20, 32768\]
-   cloud\_ssd: \[20, 32768\]
-   ephemeral\_ssd: \[5, 800\]

|
|DataDisk.n.SnapshotId|String|No|The snapshot used to create the data disk. Value range of `n`: \[1, 16\].|
|DataDisk.n.Encrypted|Boolean|No|The data disk capacity. Value range of `n`: \[1, 16\].|
|DataDisk.n.DiskName|String|No|The data disk name. Value range of `n`: \[1, 16\].|
|DataDisk.n.Description|String|No|Description of a data disk. The valid range of `n` is \[1, 16\].|
|DataDisk.n.DeleteWithInstance|String|No|Whether the data disk is released with its instance. Value range of `n`: \[1, 16\].|
|IoOptimized|String|No|Whether it is an I/O-optimized instance or not. Optional values:-   none
-   optimized

|
|NetworkInterface.1.PrimaryIpAddress|String|No|The primary private IP address of the ENI.|
|NetworkInterface.1.VSwitchId|String|No|The VSwitch ID for ENI. The instance must be in the same zone of the same VPC network as the ENI, but they may belong to different VSwitches.|
|NetworkInterface.1.SecurityGroupId|String|No|The security group ID must be one in the same VPC.|
|NetworkInterface.1.NetworkInterfaceName|String|No|ENI name.|
|NetworkInterface.1.Description|String|No|The ENI description.|
|InternetChargeType|String|No|Internet bandwidth billing method. Optional values: PayByTraffic|
|UserData|String|No|User data of the instance, which is Base64-encoded. Size of the raw data cannot exceed 16 KB.|
|KeyPairName|String|No|The name of the key pair.-   Ignore this parameter for Windows instances. It is null by default. Even if you enter this parameter, only the  `Password` content is used.
-   The password logon method for Linux instances is set to forbidden upon initialization.

|
|RamRoleName|String|No|The RAM role name of the instance. You can use the *RAM* API [ListRoles](../../../../../reseller.en-US/Developer Guide/API reference (RAM)/Role Management Interface/ListRoles.md#) to query instance RAM role names.|
|AutoReleaseTime|String|No|Instance auto release time. The time is presented using the [ISO8601](reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard and in UTC time. The format is  YYYY-MM-DDTHH:MM:SSZ. |
|SpotStrategy|String|No|The spot strategy for a Pay-As-You-Go instance. This parameter is valid and mandatory only when `InstanceChargeType` is set to `PostPaid`. Value range:-   NoSpot: Normal Pay-As-You-Go instance.
-   SpotWithPriceLimit: Sets the maximum price for a spot instance.
-   SpotAsPriceGo: The system automatically calculates the price. The maximum value is the Pay-As-You-Go price.

|
|SpotPriceLimit|Float|No|Sets the maximum hourly instance price. Supports up to three decimal places.|
|SecurityEnhancementStrategy|String|No|Whether or not to activate the security enhancement feature and install network security software free of charge. Optional values: Active | Deactive.|
|Tag.n.Key|String |No |This tag applies to instance, disk, security group, or image. The key of a tag of which n is from 1 to 20. Once you use this parameter, it cannot be a null string. It can be up to 64 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|
|Tag.n.Value|String |No |This tag applies to instance, disk, security group, or image. The value of a tag of which n is a number from 1 to 20. Once you use this parameter, it can be a null string. It can be up to 128 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|
|TemplateTag.n.Key|String |No |This tag applies to launch template. The key of a tag of which n is from 1 to 20. Once you use this parameter, it cannot be a null string. It can be up to 64 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|
|TemplateTag.n.Value|String |No |This tag applies to launch template. The value of a tag of which n is a number from 1 to 20. Once you use this parameter, it can be a null string. It can be up to 128 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|LaunchTemplateId|String|The launch instance template ID.|

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplate
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-name1
&InstanceType=ecs.cm4.6xlarge
&SecurityGroupId=sg-securitygroupid
&<Common Response Parameters>
```

**Response example** 

**XML format**

```
<CreateLaunchTemplateResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
    <LaunchTemplateId>lt-m5eiaupmvm2op9dxxxxx</LaunchTemplateId>
</CreateLaunchTemplateResponse>
```

 **JSON format** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
    "LaunchTemplateId": "lt-m5eiaupmvm2op9dxxxxx"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error messages|HTTP status code |Description|
|:---------|:-------------|:----------------|:----------|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|A required parameter is missing.|
|InvalidParameter|the parameter\(s\) provided is\(are\) invalid.|400|The specified parameter is invalid.|
|InvalidLaunchTemplateName.Malformed|The specified parameter LaunchTemplateName is not valid.|400|The specified `LaunchTemplateName` is invalid.|
|InvalidDescription.Malformed|The specified parameter “VersionDescription” is not valid.|400|The specified `VersionDescription` is invalid.|
|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|400|The raw `UserData` exceeds 16 KB.|
|InvalidUserData.Base64FormatInvalid|The specified parameter UserData must be base64 encoded.|400|`UserData` must be Base64-encoded.|
|LaunchTemplateLimitExceed|The maximum number of templates is exceeded.|403|You can create up to 30 instance launch templates per region.|
|LaunchTemplateName.Duplicated|The specified LaunchTemplateName “\{0\}” already exist.|403|The specified `LaunchTemplateName` already exists.|
|InnerServiceFailed|call inner service failed|403|An internal server error.|

