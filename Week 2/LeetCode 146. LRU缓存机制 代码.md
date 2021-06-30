```C++

// C++

class LRUCache {
    
    // 初始化
    private class Node{
        int key;
        int value;
        Node pre;
        Node next;
    }

    private HashMap<Integer, Node> map;
    //设置链表保护节点
    private Node head;
    private Node tail;
    // 初始化容量capacity
    private int capacity;

    public LRUCache(int capacity) {
        // 初始化capacity
        this.capacity = capacity;
        // 创建hashmap对象map，integer类型的key和node类型的value
        this.map = new HashMap<Integer, Node>();
        // 双向链表初始化，带有保护节点
        head = new Node();
        tail = new Node();
        // 将head与tail双向连接
        head.next = tail;
        tail.pre = head;
    }
    
    // 访问双向链表
    /* 这里需要将双向链表的访问操作的复杂度降至O(1)
       利用hashmap的key-value结构get(key)方法获取key对应的value，即node
    */
    public int get(int key) {
        // 如果关键字key不存在于缓存中，返回-1
        if (this.map.containsKey(key) == false) return -1; // 检查hashmap中是否存在指定key对应的映射关系
        // 关键字key存在于缓存中，先找到其对应的node
        Node node = map.get(key);
        // 将node从现双向链表和hashmap中删除
        this.removeFromList(node);
        // 将node重新插入到hashmap和双向链表的头部
        this.insertToListHead(node.key, node.value);
        // 返回关键字key的值
        return node.value;
    }

    // 更新双向链表
    public void put(int key, int value) {
        // 如果关键字key存在于缓存中，更新数据值并将其重新插入到双向链表和hashmap的头部
        if (this.map.containsKey(key)) {
            // 关键字key存在于缓存中，先找到其对应的node
            Node node = this.map.get(key);
            // 将node从现双向链表和hashmap中删除
            this.removeFromList(node);
            // 将node重新插入到hashmap和双向链表的头部
            this.insertToListHead(key, value);
        }else{
            // 如果关键字key不存在于缓存中，在双向链表头部插入新的节点
            this.insertToListHead(key, value);
        }
        // 考虑容量上限问题
        // 如果hashmap中key-value pair的数量超出缓存容量，从双向链表和hashmap中删除尾部node和其对应的key-value pair
        if (this.map.size() > capacity){
            // 删除尾部node，即删除尾部保护节点的前一个节点
            this.removeFromList(tail.pre);
        }
    }
    
    // 模板操作：将双向链表中的一个节点删除（同时更新hashmap）
    // 等价于将待删节点的前一个node指向其后一个node，后一个node指向其前一个node，
    private void removeFromList(Node node){
        // 待删节点的前一个node指向其后一个node
        node.pre.next = node.next;
        // 待删节点的后一个node指向其前一个node
        node.next.pre = node.pre;
        // 同时更新hashmap，将node从中删除
        this.map.remove(node.key);
    }

    // 模板操作：在双向链表的头部插入一个节点（同时更新hashmap，返回访问get时已在缓存中的node key-value）
    // 等价于在保护节点head与head.next节点之间插入一个新节点
    private Node insertToListHead(Integer key, Integer value){
        // 新增节点的key-value
        Node node = new Node();
        node.key = key;
        node.value = value;
        // 新增的node指向保护节点原本的后一个node，即head.next
        node.next = head.next;
        // 保护节点原本的后一个node，即head.next，指向新增的node
        head.next.pre = node;
        // 保护节点head的后一个node指向新增的node
        head.next = node;
        // 后一个node指向新增的node指向保护节点head
        node.pre = head;
        // 更新hashmap，在hashmap中增加新的映射关系key指向node
        this.map.put(key, node);
        return node;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */

```
