Set接口作为Java集合框架的核心组成部分，与List形成鲜明对比，其核心特征在于**元素唯一性**。与Map接口不同，Set仅存储单一元素而非键值对，但底层实现与Map存在技术同源性。

## HashSet
`HashSet` 是一个底层基于 `HashMap` 实现的Set集合，内部维护一个 `HashMap<E, Object>`，添加的元素作为 `HashMap` 的 `key` ，`value` 是一个空对象。
- **特点**
	1. 插入和查询效率高。  
	2. 非线程安全。  
	3. 自动去重。
## LinkedHashSet

## TreeSet