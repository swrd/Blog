### ����������
#### ��������
���ú���Ĳ������ˣ���Ч��֤��Ⱥ���ݴ��ԡ���֤��Ⱥ���κ�һ̨����崵�����Ⱥ�����������ṩ��д����
`���崵���һ���������������÷���������ô���еĿ��ֺ�Ǩ�ƶ�����ͣ����������ͣ��Ƭ������������Ӱ�켯Ⱥ�����������������÷������ָ��󣬾��ܼ������ֺ�Ǩ���ˡ�`

> �ڷ����κη�Ƭ����ʱ�����е����÷������������ߡ�

#### ����ע������
##### �����м��Ͻ��з�Ƭ
![](index_files/89b3b045-6bc2-4eb8-8f2a-d6ec30df7636.jpg)
##### �ڳ�ʼ����ʱԤ��ֿ�
![](index_files/218b9582-64b0-416d-84d2-93dcecded370.jpg)
![](index_files/2038a0b6-9563-4b41-8bd9-4bb09d38a426.jpg)

#### ����
##### ɾ����Ƭ
ɾ����Ƭ������ͨ��removeshard����ɾ����
```
> use admin
> db.runCommand({removeshard:"shard-1/arete:30100,arete:30101"})
{
 "msg":"draining started successfully",
 "state":"started",
 "shard":"shard-1-test-rs",
 "ok":1
}
```
�����ٴ����и����������ɾ�����̣�
```
> use admin
> db.runCommand({removeshard:"shard-1/arete:30100,arete:30101"})
{
 "msg":"draining ongoing",
 "state":"ongoing",
 "remaining":{
    "chunks":376,
    "dbs":3
 },
 "ok":1
}
```

һ����Ƭ����գ��㻹Ҫȷ�Ͻ�Ҫɾ���ķ�Ƭ�������ݿ������Ƭ������ͨ����ѯconfig.databases���ϵķ�Ƭ��Ա�����;
```
> use config
> db.databases.find()
{ "_id" : "cloud-docs", "primary" : "shardA", "partitioned" : true }
{ "_id" : "test", "primary" : "shardB", "partitioned" : false }
{ "_id" : "bs", "primary" : "shard3", "partitioned" : true }
{ "_id" : "cheat_history", "primary" : "shard3", "partitioned" : true }
{ "_id" : "user_identify", "primary" : "shard3", "partitioned" : false }
{ "_id" : "guilds", "primary" : "shard3", "partitioned" : true }
```
���п��Կ�����cloud-docs���ݿ�����shardA����test���ݿ�������shardB����Ϊ����ɾ��shardB��������Ҫ�ı�test���ݿ�����ڵ㡣Ϊ�ˣ�����ʹ��moveprimary���`����������Ǩ���ڷ�Ƭ��ʣ��ķ�sharding����`��:
```
> db.runCommand({moveprimary:"test",to:"shard-0-test-rs"});
```
> һ��Ҫ�ȷ�Ƭ����Ǩ����ɺ���Ǩ�ƷǷ�Ƭ�����ݿ⡣

��Ǩ����ɺ�
```
> use admin
> db.runCommand({removeshard:"shard-1/arete:30100,arete:30101"})
{
 "msg":"remove shard completed successfully",
 "state":"completed",
 "host":"arete:30100",
 "ok":1
}
```


