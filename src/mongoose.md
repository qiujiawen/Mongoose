# Mongoose 简介

### 基础

*Schema:* 一种以文件形式存储的数据库模型骨架，不具备数据库的操作能力.

*Model:* 由Schema发布生成的模型，具有抽象属性和数据库操作能力.

*Entity:* 由Model创建的实例,也能操作数据库

##### 三者之间的关联：
Schema 生成 Model，Model 创造 Entity，Model 和 Entity 都可对数据库操作造成影响，但 Model 比 Entity 更具操作性。

### Mongodb

学习 mongodb 的过程中需要熟悉几个名词以及他们对应的关系型数据库名词。

<table>
  <tr>
    <th>关系型数据库</th>
    <th>mongodb</th>
  </tr>
  <tr>
    <td>table</td>
    <td>collection</td>
  </tr>
  <tr>
    <td>row</td>
    <td>document</td>
  </tr>
  <tr>
    <td>column</td>
    <td>index</td>
  </tr>
  <tr>
    <td>table joins</td>
    <td>populate</td>
  </tr>
  <tr>
    <td>primary key</td>
    <td>_id_</td>
  </tr>
</table>