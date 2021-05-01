# jq

最简单的jq程序是表达式"."，它不改变输入，但可以将其优美地输出，便于阅读和理解

echo '{"foo": 0}' | jq .

{
  "foo": 0
}

➜  configmap  echo '{"foo": 0}' | jq .foo

0

length函数

echo '{"name": "test", "age": 33}' | jq '.name | length'
4

获取指定字段的值：
echo '{"name": "test", "age": 33}' | jq '.name'

"test"


[index]

输出列表中的第一个元素，可以使用[index]：


示例JOSN

cat apinfo.json

[{"hostCompany":"Beijing ALex Technology","hostModel":"moto","hostsn":"01051658823","mac":"5D:2F:47:2E:F3:8E","cpuModel":"999","cpuSN":"000000","memoryModel":"abcdefg","memorySN":"000000","boardSN":"0101011223133","networkCardMac":"5D:2F:47:2E:F3:8E","lowFreModel":"A7655","lowFreSN":"000000","hignFreModel":"AR9582","hignFreSN":"000000","hardVersion":"1.0","firmwareVersion":"1.0"}]

jq支持管道线 |，它如同linux命令中的管道线——把前面命令的输出当作是后面命令的输入。如下命令把.[0]作为{…}的输入，进而访问嵌套的属性


cat apinfo.json|jq '.[0] | .hostCompany, .firmwareVersion'

"Beijing ALex Technology"
"1.0"


自定义key

在{}中，冒号前面的名字是映射的名称，你可以任意修改,如这里的name,fireware
 cat apinfo.json|jq '.[0] | {name:.hostCompany,fireware:.firmwareVersion}'
{
  "name": "Beijing ALex Technology",
  "fireware": "1.0"
}

cat apinfo.json|jq '.[0] | {name:.hostCompany,city:.firmwareVersion,mac:.mac}'


{
  "name": "Beijing ALex Technology",
  "city": "1.0",
  "mac": "5D:2F:47:2E:F3:8E"
}

cat apinfo.json|jq '.[] | .mac'

"5D:2F:47:2E:F3:8E"

cat apinfo.json|jq '.[] | .mac, .cpuModel'

"5D:2F:47:2E:F3:8E"
"999"

