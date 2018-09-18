## 1.1 rule.xml
### 1.1.1 相关文件 

这部分与rule.dtd和rule.xml相关。  
  
rule.dtd定义解析规则，仅与开发相关。如有疑问，请参看[xml_dtd_intro](https://www.w3schools.com/xml/xml_dtd_intro.asp)。
  
rule.xml定义实际用到的分区算法的配置，它包括如下两类信息：  

#### A.分区规则定义
分区规则定义有如下形式：


+ tableRule

<table >
<tr>
<th >配置名称</th>
<th >配置内容</th>
<th >可设多值</th>
<th >说明</th>
</tr>
<tr>
<td >name</td>
<td >规则名称</td>
<td >否</td>
<td >tableRule属性，该规则名将被schema.xml中表配置引用,必须在整个文件中唯一</td>
</tr>
<tr>
<td >rule</td>
<td >规则详情</td>
<td >否</td>
<td >rule子结构</td>
</tr>
</table>


### 1.1.2 支持的分区算法  
目前，已支持的分区算法有: hash, stringhash, enum, numberrange, patternrange, date，jumpstringhash.  
	
#### 1.hash分区算法

function的 class属性设置为“hash”或者“com.actiontech.dble.route.function.PartitionByLong"的分区规则应用该算法。具体配置如下：

```  
<function name="hashLong" class="hash">
      <property name="partitionCount">C1[,C2, ...Cn]</property>
      <property name="partitionLength">L1[,L2, ...Ln]</property>
</function>
``` 

**partitionCount**:指定分区的区间数， 具体为 C1 [+C2 + ... + Cn].   

**partitionLength**:指定各区间长度， 具体区间划分为 [0, L1),   [L1, 2*L1),  ...,  [(C1-1)*L1, C1*L1),   [C1*L1, C1*L1+L2),  [C1*L1+L2, C1*L1+2*L2), ... 其中，每一个区间对应一个数据节点。  
  
   
<br/>
   
例如，配置F1：  
``` 
<property name="partitionCount">2,3</property>
<property name="partitionLength">100,50</property>
``` 

将划分如下的分区：
[0 , 100)  
[100, 200)  
[200, 250)  
[250, 300)  
[300, 350)  
  
<br/>

再如,配置F2:

``` 
<property name="partitionCount">2</property>
<property name="partitionLength">1000</property>
``` 