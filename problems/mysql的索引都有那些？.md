1. **B-Tree索引**：
   - 这是最常见的索引类型，它适用于全键值、键值范围和键值排序操作。
   - 大部分MySQL存储引擎都支持B-Tree索引，包括InnoDB、MyISAM、Memory等。
2. **哈希索引**：
   - 哈希索引基于哈希表实现，只有精确匹配索引所有列的查询才有效。
   - 它们通常用于等值比较，如使用`=`, `IN()`, 和`<=>`操作符的查询。
   - Memory存储引擎使用哈希索引作为默认索引类型。
3. **FULLTEXT（全文）索引**：
   - 全文索引用于对文本内容进行全文搜索。
   - 它只适用于CHAR、VARCHAR或TEXT列。
   - InnoDB和MyISAM存储引擎支持全文索引。