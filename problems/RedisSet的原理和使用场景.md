### Redis Set 原理：

- Redis的Set类型是一个无序、不重复的集合，内部使用哈希表实现，保证了集合中元素的唯一性。
- Set类型支持添加、删除、判断元素是否存在等操作，时间复杂度为O(1)。
- Redis还提供了丰富的集合运算命令，如求交集、并集、差集等，方便对多个集合进行操作。

### Redis Set 使用场景：

1. 标签系统：Set类型适合用于存储对象的标签信息，每个对象可以关联一个或多个标签，通过集合操作实现标签之间的交集、并集查询。
2. 好友关系：可以将用户的好友列表存储在Set中，利用集合运算命令快速实现共同好友、推荐好友等功能。
3. 唯一性校验：通过Set类型存储数据的唯一性信息，可以快速进行去重操作，确保数据的唯一性。
4. 点赞/收藏功能：可以利用Set类型记录用户点赞或收藏的内容，确保每个用户对同一内容只能进行一次操作。